# Troubleshooting

## `.env` is missing

Meaning:
- The project root does not contain the configuration file this skill expects.

Fix:
- create `.env`
- add `YUNXIAO_TOKEN=<your token>`

## `YUNXIAO_TOKEN` is missing

Meaning:
- The skill cannot authenticate to Codeup.

Fix:
- add `YUNXIAO_TOKEN` to `.env`
- retry the repository creation step

## `organization_id` is missing

Meaning:
- The skill cannot determine which Codeup organization should own the new repository.

Fix:
- provide `organization_id` explicitly
- or configure the environment or project context so the skill can read it

## Repository creation redirects to login

Meaning:
- The request may be using the wrong API domain, or the token is not being accepted by the central-edition OpenAPI endpoint.

Fix:
- use `openapi-rdc.aliyuncs.com` for central-edition OpenAPI calls
- keep `codeup.aliyun.com` only for Git remote URLs and web access
- verify the token has Codeup repository permissions

## Repository already exists

Meaning:
- The normalized local folder name collides with an existing remote repository.

Fix:
- choose a different repository name
- or connect the local folder to the existing repository deliberately

## Local Git already initialized

Meaning:
- The project is not a fresh bootstrap target.

Fix:
- inspect current branch and remotes
- adapt the existing repository state instead of reinitializing

## SSH remote cannot push

Meaning:
- SSH auth may be missing, or the remote URL may be wrong.

Fix:
- test SSH access to the Git host
- verify the remote URL
- verify repository write permissions

## First push rejected

Meaning:
- The remote may already contain commits, or the local branch/remotes are misaligned.

Fix:
- inspect remote default branch and current commits
- decide whether to pull/rebase, force push, or reconnect the local repo to a new remote
