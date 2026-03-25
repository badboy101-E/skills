# Publish Workflow

## Inputs to collect

Resolve these values before generating final commands:

- `<local_skill_path>`
- `<target_repo_url>`
- `<target_clone_path>`
- `<target_branch>`
- `<skill_name>`

Typical defaults:

- `<target_branch>`: `main`
- `<target_clone_path>`: a folder inside the current workspace

## Inspect the target repository

Check whether the repository exists and what the default branch is:

```bash
git ls-remote <target_repo_url>
```

Clone it locally:

```bash
git clone <target_repo_url> <target_clone_path>
```

Inspect current files before copying the skill:

```bash
find <target_clone_path> -maxdepth 2 -type f | sort
git -C <target_clone_path> status --short
```

## Copy the skill into the repository

If the repository is a dedicated skills repo and has no stricter layout:

```bash
cp -R <local_skill_path> <target_clone_path>/
```

Then inspect the copied structure:

```bash
find <target_clone_path>/<skill_name> -maxdepth 2 -type f | sort
git -C <target_clone_path> status --short
```

## Commit the skill

Keep the commit message specific:

```bash
git -C <target_clone_path> add <skill_name>
git -C <target_clone_path> commit -m "Add <skill_name> skill"
```

If repository-level documentation changed too, include it in a second commit or in the same focused commit if both changes are part of the same publish step.

## Push over SSH

Once the remote uses SSH:

```bash
git -C <target_clone_path> push origin <target_branch>
```
