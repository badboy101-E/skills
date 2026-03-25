---
name: volcengine-docker-cd
description: Run a Docker-based continuous delivery workflow for any project on a Volcengine container registry, including versioned image builds, tagging, pushing, remote Docker Compose deployment, and rollback guidance. Use when Codex needs to package a project as a Docker image, publish a release to Volcengine, deploy that release on a remote Linux server, diagnose registry/auth/manifest issues, or switch a deployment back to an earlier image tag.
---

# Volcengine Docker CD

Use this skill to turn an existing project into a repeatable Docker release workflow for Volcengine. Prefer reading the current project's `Dockerfile`, Compose files, image tags, ports, and required environment variables instead of guessing or hardcoding project-specific names.

## Workflow

1. Inspect the project before proposing commands.
Check for `Dockerfile`, `docker-compose.yml` or `compose.yaml`, exposed ports, environment variables, and any existing image tags.

2. Resolve release parameters from project context.
Identify or ask for only the minimum required values:
- registry host
- repository path
- image tag
- rollback target tag when applicable
- service name
- host/container port mapping
- runtime environment variables

3. Choose the build strategy.
Use multi-architecture `docker buildx build --platform linux/amd64,linux/arm64 --push` by default when the image will run on remote Linux servers and the local machine may be Apple Silicon. Only use single-platform builds when the target platform is known and constrained.

4. Prefer remote deployment by pulling a published image.
For remote servers, generate `docker compose` instructions that reference the registry image directly. Do not require rebuilding on the server unless the user explicitly wants that workflow.

5. Treat version tags as first-class release artifacts.
Every formal release should have a unique immutable image tag. Recommend an explicit release tag such as `1.0.0`, `2026.03.25`, or a Git SHA tag, and treat `latest` only as an optional convenience tag.

6. Keep verification project-specific.
Do not assume `/healthz` or any fixed application endpoint. If the project already defines a verification command, reuse it. Otherwise provide a generic deployment verification sequence: container status, logs, and a user-supplied functional request.

## Rules

- Parameterize names and ports. Never hardcode a service name, image name, repository path, or port unless the user or project files define it.
- Prefer the current project's actual configuration over examples from past projects.
- Formal releases must use a unique image tag. Do not recommend `latest` as the only production deployment tag.
- Treat rollback as part of CD. Prefer changing the deployed image tag back to a previously published version over rebuilding an older code state on the server.
- If a remote deployment failed with a manifest mismatch, treat it as an architecture problem first.
- If a push failed with an auth or token error, treat it as a registry login or permission problem first.
- If Compose tries to pull a local image name from Docker Hub, add `build:` or use the fully qualified registry image explicitly.
- Keep secrets out of committed Compose files. Prefer `${ENV_VAR}` interpolation or `.env` files for runtime secrets.

## References

- For command templates and release sequencing, read [references/release-workflow.md](references/release-workflow.md).
- For remote server deployment with Compose, read [references/compose-deploy.md](references/compose-deploy.md).
- For common Docker/registry/architecture failures, read [references/troubleshooting.md](references/troubleshooting.md).

## Output Expectations

When responding, prefer:
- concrete commands with placeholders filled from the current project
- explicit version tags and, when helpful, a matching rollback tag
- brief notes about why a specific build strategy was chosen
- one delivery path at a time: local build, registry push, remote Compose deploy, or rollback
- targeted troubleshooting tied to the exact error text
