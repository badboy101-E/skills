# Release Workflow

## Inputs to collect

Resolve these values from the project or the user before generating final commands:

- `<registry_host>`
- `<repository_path>`
- `<local_image>`
- `<image_tag>`
- `<rollback_tag>`
- `<dockerfile_path>`
- `<build_context>`
- `<target_platforms>`

Common defaults:

- `<target_platforms>`: `linux/amd64,linux/arm64`
- `<dockerfile_path>`: `Dockerfile`
- `<build_context>`: `.`

## Inspect before building

Use project files first:

```bash
rg --files .
sed -n '1,200p' Dockerfile
sed -n '1,220p' docker-compose.yml
```

If the user already built an image, inspect local tags:

```bash
docker images --format '{{.Repository}}:{{.Tag}} {{.ID}}'
docker image inspect <local_image>:<image_tag> --format '{{.Os}}/{{.Architecture}}'
```

## Local build only

Use this only when the user wants a local image and no registry push yet:

```bash
docker build -t <local_image>:<image_tag> -f <dockerfile_path> <build_context>
```

## Preferred publish flow

Use `buildx` when the image will be pulled on a remote Linux server, especially if the local machine may be Apple Silicon:

```bash
docker login --username='<registry_username>' <registry_host>
docker buildx build \
  --platform <target_platforms> \
  -t <registry_host>/<repository_path>:<image_tag> \
  --push \
  -f <dockerfile_path> \
  <build_context>
```

If the user also wants `latest`, push both tags in the same release:

```bash
docker buildx build \
  --platform <target_platforms> \
  -t <registry_host>/<repository_path>:<image_tag> \
  -t <registry_host>/<repository_path>:latest \
  --push \
  -f <dockerfile_path> \
  <build_context>
```

If the user wants a traceable release, add a second immutable tag such as a Git SHA:

```bash
docker buildx build \
  --platform <target_platforms> \
  -t <registry_host>/<repository_path>:<image_tag> \
  -t <registry_host>/<repository_path>:<git_sha_tag> \
  --push \
  -f <dockerfile_path> \
  <build_context>
```

## Tag and push an already-built local image

Use this only when the local image is known-good and platform compatibility is acceptable:

```bash
docker login --username='<registry_username>' <registry_host>
docker tag <local_image>:<image_tag> <registry_host>/<repository_path>:<image_tag>
docker push <registry_host>/<repository_path>:<image_tag>
```

## Versioning guidance

- Prefer explicit semantic-style tags such as `1.0.0`, `1.0.1`, or `2026.03.25`.
- Consider also publishing a Git SHA tag for traceability.
- Use `latest` only as an additional convenience tag, not the only release tag.
- When a remote server is pinned to a version, update the Compose file deliberately instead of silently moving tags.
- Keep previously deployed tags in the registry so they can be used for quick rollback.

## Release record guidance

Encourage the user to capture, at minimum:

- deployment environment
- release tag
- optional Git SHA tag
- deployment time
- operator or automation name

This can live in CI logs, deployment notes, or a release record file. The key goal is to make rollback targets obvious.
