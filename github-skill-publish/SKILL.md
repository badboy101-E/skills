---
name: github-skill-publish
description: Publish a locally created Codex skill to a GitHub repository, especially when the repository is used to store self-built skills and the preferred delivery path is Git over SSH. Use when Codex needs to clone or inspect a target GitHub repository, copy a local skill directory into it, update repository-level documentation such as README indexes, switch the remote from HTTPS to SSH, commit the new skill, push it to GitHub, or diagnose authentication and push failures.
---

# GitHub Skill Publish

Use this skill to package and publish an existing local skill into a GitHub repository that stores reusable skills. Prefer SSH-based Git operations once the machine has a working GitHub SSH key.

## Workflow

1. Inspect the source skill and the target repository.
Confirm the local skill path, the target GitHub repository URL, the default branch, and whether the repository already has a skill catalog or README.

2. Choose the repository placement.
If the repository is a dedicated skills repo, prefer copying the whole skill directory into the repo root. If the repository already has a specific layout, follow that layout instead of inventing a new one.

3. Prefer SSH for write operations.
Read-only inspection can use HTTPS, but pushing should use SSH if possible. Verify `ssh -T git@github.com` before switching remotes and pushing.

4. Keep repository docs in sync.
If the repository has a top-level README or skill index, update it so the new skill is discoverable. Treat repository overview maintenance as part of the publishing flow.

5. Commit only the intended skill changes.
Do not mix unrelated files into the publish commit. Keep the commit message specific to the skill addition or repository index update.

## Rules

- Treat the source skill as the canonical artifact. Copy it without rewriting names or folder structure unless the repository requires a different convention.
- Prefer cloning the target repository into the current workspace before editing it.
- Use SSH remotes for push operations when GitHub SSH auth is available.
- If the repository is nearly empty, add the skill directory directly and optionally create a repository README if the user wants a browsable landing page.
- If the push fails, distinguish between auth failures, missing repository permissions, and remote URL misconfiguration.
- Keep the repository index human-readable. Favor short summaries and a table or list of skills when the repo will continue to grow.

## References

- For the end-to-end publish sequence, read [references/publish-workflow.md](references/publish-workflow.md).
- For SSH setup, remote switching, and auth checks, read [references/ssh-and-auth.md](references/ssh-and-auth.md).
- For repository README and skill catalog updates, read [references/repo-readme.md](references/repo-readme.md).

## Output Expectations

When responding, prefer:
- concrete Git and filesystem commands filled from the current repo and skill paths
- one publishing path at a time: inspect, clone, copy, commit, push, or troubleshoot
- precise guidance for SSH versus HTTPS behavior
- repository README updates that make future skills easy to add
