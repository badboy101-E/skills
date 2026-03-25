# Compose Deploy

## When to use this path

Use this path when the image is already published to a registry and the user wants a fresh remote Linux server to pull and run it with Docker Compose.

## Files to prepare on the server

Create a deployment directory and place:

- `docker-compose.yml`
- `.env` if runtime secrets or variables are needed

## Compose template

Replace placeholders with project-specific values:

```yaml
services:
  <service_name>:
    image: <registry_host>/<repository_path>:<image_tag>
    container_name: <service_name>
    ports:
      - "<host_port>:<container_port>"
    environment:
      <ENV_KEY_1>: ${<ENV_KEY_1>}
      <ENV_KEY_2>: ${<ENV_KEY_2>}
    restart: unless-stopped
```

Only include environment variables the app actually needs. If the project already has a Compose file, adapt it rather than replacing it blindly.

## .env template

```env
<ENV_KEY_1>=<value>
<ENV_KEY_2>=<value>
```

Do not commit production secrets unless the user explicitly wants that tradeoff.

## Remote deploy sequence

```bash
docker login --username='<registry_username>' <registry_host>
docker compose pull
docker compose up -d
docker compose ps
docker compose logs --tail=200
```

If the image tag changed:

```bash
docker compose pull
docker compose up -d
```

If the user wants a clean recreation:

```bash
docker compose up -d --force-recreate
```

## Rollback

Treat rollback as a tag switch, not a rebuild.

1. Change the Compose image reference from the current release tag to `<rollback_tag>`.
2. Pull the rollback image.
3. Recreate the service.

Example:

```bash
docker compose pull
docker compose up -d
docker compose ps
docker compose logs --tail=200
```

If the user wants explicit rollback guidance, tell them which tag is current and which tag will be restored.

## Verification

Because application interfaces differ across projects, choose verification in this order:

1. `docker compose ps`
2. `docker compose logs --tail=200`
3. The project's existing health or smoke-test command
4. A user-supplied business request against the deployed endpoint
