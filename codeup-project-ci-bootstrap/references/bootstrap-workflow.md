# Bootstrap Workflow

## Preconditions

- The user has already created or chosen the local project directory.
- The project root contains a `.env` file with `YUNXIAO_TOKEN`.
- The user or environment can provide `organization_id`.
- The machine has Git available.
- SSH is the preferred remote protocol.

## Inspect local state

```bash
pwd
ls -la
test -f .env && echo ".env exists"
test -d .git && echo "git already initialized"
```

Derive the repository name from the current directory:

```bash
basename "$PWD"
```

## Create the remote repository

Read `YUNXIAO_TOKEN` from `.env`, resolve `organization_id`, then call the central-edition Codeup OpenAPI endpoint. Use `openapi-rdc.aliyuncs.com` as the default OpenAPI domain unless the user provides a different central-edition endpoint.

When generating the request, include:

- `organization_id`
- normalized repository name
- visibility `private`
- default branch `main` if supported by the request body

If the repository already exists, stop and tell the user instead of guessing the next action.

## Initialize local Git

Only when `.git` does not already exist:

```bash
git init -b main
```

If `.git` already exists, inspect the current branch and remotes before making changes:

```bash
git branch --show-current
git remote -v
```

## Generate starter files

Use the templates under `assets/templates/` to create:

- `README.md`
- `.gitignore`
- `.env.example`
- `ci/README.md`
- `scripts/check.sh`
- `scripts/test.sh`
- `scripts/build.sh`

Keep these files generic and editable.

## Configure SSH remote

Set or update `origin` with the repository's SSH URL.

Typical sequence:

```bash
git remote -v
git remote add origin <ssh-url>
```

Or, if `origin` exists but is wrong:

```bash
git remote set-url origin <ssh-url>
```

## First commit and push

```bash
git add .
git commit -m "Initial project bootstrap"
git push -u origin main
```
