---
name: codeup-project-ci-bootstrap
description: Bootstrap a new local project into a CI-ready Git repository backed by a central-edition Alibaba Cloud Codeup repository. Use when Codex needs to start from an already created local project folder, read Codeup credentials from a local .env file, create a private remote repository through the central-edition OpenAPI endpoint, initialize Git, generate minimal CI starter files, configure an SSH remote, and push the first commit to the main branch. Treat organization identifiers and platform settings as user- or environment-supplied parameters rather than hardcoded personal values.
---

# Codeup Project CI Bootstrap

Use this skill when a project folder already exists locally and needs to be turned into a clean starting point for CI/CD. This skill is responsible for repository creation, Git initialization, and minimal CI bootstrap files. It does not generate Docker or deployment files; those belong in a later CD workflow.

## Workflow

1. Start from the current local project directory.
Do not choose the project path for the user. Assume the user has already created or chosen the local folder.

2. Read configuration from the local `.env`.
Load `YUNXIAO_TOKEN` from `.env` in the project root. Use this token for Codeup API requests. If `.env` is missing or `YUNXIAO_TOKEN` is absent, stop and report the missing prerequisite clearly.

3. Derive the repository name from the local folder.
Use the current directory name as the default repository name, then normalize it for remote repository creation. Prefer kebab-case and keep it as close to the local name as possible.

4. Create the remote repository on central-edition Codeup.
Use:
- OpenAPI domain default: `openapi-rdc.aliyuncs.com`
- Git host default: `codeup.aliyun.com`
- organization id: user- or environment-supplied
- visibility: `private`
- branch: `main`
- no namespace by default
- no remote README initialization by default

5. Initialize local Git if needed.
Create `.git` only when it does not already exist. Set the initial branch to `main`.

6. Generate minimal CI starter files.
Generate only the basic bootstrap files:
- `README.md`
- `.gitignore`
- `.env.example`
- `ci/README.md`
- `scripts/check.sh`
- `scripts/test.sh`
- `scripts/build.sh`

7. Configure the remote with SSH.
Prefer SSH for the Codeup remote URL. Reuse an existing `origin` only if it already points to the intended repository; otherwise set or replace it deliberately.

8. Create the first commit and push.
Stage the generated files and current project contents, create an initial commit, and push to `origin main` when the user wants the bootstrap completed end-to-end.

## Rules

- Treat this as a CI bootstrap skill, not a deployment skill.
- Do not generate `Dockerfile`, `docker-compose.yml`, or other CD assets.
- Read `YUNXIAO_TOKEN` from `.env`, not from inline hardcoded values.
- Read `organization_id` from user input, project context, or environment configuration. Do not hardcode a personal organization id in a public version of this skill.
- Use the local directory name as the default repository name source.
- Keep the default repository private.
- Prefer SSH for Git remote operations.
- Generate minimal, editable starter files rather than opinionated application templates.
- If the local repository already exists, adapt to it instead of reinitializing blindly.
- If the remote repository already exists, stop and explain the collision rather than assuming overwrite behavior.

## References

- For Codeup API details and required request fields, read [references/codeup-api.md](references/codeup-api.md).
- For the full bootstrap sequence, read [references/bootstrap-workflow.md](references/bootstrap-workflow.md).
- For starter file generation, read [references/file-generation.md](references/file-generation.md).
- For common failures, read [references/troubleshooting.md](references/troubleshooting.md).

## Assets

Use the templates in `assets/templates/` when generating starter files. Keep them minimal and easy to edit after initialization.

## Output Expectations

When responding, prefer:
- concrete commands filled from the current directory and repository name
- clear notes about which files will be created
- a single bootstrap path from local folder to pushed remote repository
- targeted fixes when Codeup API, `.env`, SSH, or Git state causes failures
