# SSH And Auth

## Prefer SSH for GitHub pushes

Use HTTPS for simple read-only checks if convenient, but prefer SSH for write operations to avoid repeated username/token prompts.

## Test SSH auth

```bash
ssh -T git@github.com
```

Expected success output:

```text
Hi <github-username>! You've successfully authenticated, but GitHub does not provide shell access.
```

On first connection, GitHub may ask to trust the host fingerprint. Accept it only if it matches GitHub's expected host key.

## Inspect the current remote

```bash
git -C <target_clone_path> remote -v
```

## Switch from HTTPS to SSH

```bash
git -C <target_clone_path> remote set-url origin git@github.com:<owner>/<repo>.git
git -C <target_clone_path> remote -v
```

## Common auth problems

### HTTPS push prompts for username/password

Meaning:
- The remote is still HTTPS.

Fix:
- switch the remote to SSH
- or use a GitHub Personal Access Token if HTTPS must remain

### SSH auth succeeds, but push is rejected

Meaning:
- The key is valid, but the GitHub account may not have write access to the repository or branch.

Fix:
- verify repository permissions
- verify branch protections
- verify the remote points to the intended repository
