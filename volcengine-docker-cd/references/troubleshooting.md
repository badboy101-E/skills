# Troubleshooting

## `no matching manifest for linux/amd64`

Meaning:
- The pushed image does not include the remote server's platform.

Typical cause:
- The image was built on Apple Silicon with plain `docker build` and pushed as `linux/arm64` only.

Fix:

```bash
docker buildx build \
  --platform linux/amd64,linux/arm64 \
  -t <registry_host>/<repository_path>:<image_tag> \
  --push \
  <build_context>
```

## `invalid_token: authorization failed`

Meaning:
- Registry authentication failed, or the login lacks push permission to the target repository.

Fix:

```bash
docker login --username='<registry_username>' <registry_host>
docker push <registry_host>/<repository_path>:<image_tag>
```

Also verify the repository path exists and is spelled correctly.

## Release deployed, but rollback target is unclear

Meaning:
- The deployment uses floating tags or there is no release record tying environments to image versions.

Fix:
- deploy with an explicit immutable tag
- preserve prior release tags in the registry
- record the deployed tag and optional Git SHA for each environment

## Compose tries to pull a local image from Docker Hub

Meaning:
- The Compose file references `image: some-name:tag`, but the image is not available locally in the environment where Compose is running.

Fix options:
- Add `build:` so Compose builds from the local project.
- Use a fully qualified registry image, such as `<registry_host>/<repository_path>:<image_tag>`.

## Docker Hub or mirror fetch failures during `docker build`

Symptoms:
- timeouts
- `401 Unauthorized`
- `403 Forbidden`
- mirror-specific failures when resolving a base image

Fix:
- verify the configured Docker mirror
- retry with a known-good mirror or a different base image source
- pre-pull the base image to confirm registry access before rebuilding

## Docker Desktop `.raw` file looks huge

Meaning:
- The file often reflects virtual disk allocation or upper bounds, not actual live image usage.

Check real usage with:

```bash
docker system df -v
du -sh <docker_desktop_storage_dir>
```

Use Docker cleanup commands instead of deleting the `.raw` file directly.
