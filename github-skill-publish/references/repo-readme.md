# Repository README

## When to update the README

Update the repository README when:

- the repository is intended as a browsable skills catalog
- a new skill should be discoverable from the repo root
- the repo is sparse and needs a landing page

## Good repository README traits

- explain what the repository is for
- state that the skills are real, tested, and reusable
- list current skills in a format that scales
- leave room for future additions

## Suggested structure

For a repository that will grow over time, prefer:

1. short repository positioning
2. why the repository exists
3. a skill catalog table
4. notes for the currently available skills
5. roadmap or future directions
6. usage or adaptation notes

## Skill catalog pattern

Use a small table for scanability:

```md
| Skill | Type | Use Case | Core Capabilities |
| --- | --- | --- | --- |
| [`example-skill`](./example-skill) | Deploy / CI | Publish and deploy services | Build, push, deploy, rollback |
```

## Update rule

When adding a new skill to a growing repo:

- add the skill to the catalog table
- add or update a short note for the new skill
- keep the README concise enough that future edits stay easy
