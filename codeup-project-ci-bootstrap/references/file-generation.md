# File Generation

## Goal

Generate the smallest useful set of CI bootstrap files without forcing an application template or deployment strategy.

## Files to create

### `README.md`

Use a minimal project README:

- project name
- one-line project description placeholder
- local development placeholder
- CI note placeholder

### `.gitignore`

Include common ignores that fit general development:

- `.env`
- `.DS_Store`
- `__pycache__/`
- `.venv/`
- `node_modules/`
- IDE noise where appropriate

### `.env.example`

Include a placeholder for:

```env
YUNXIAO_TOKEN=
```

Add space for project-specific variables later.

### `ci/README.md`

Explain that this directory holds CI-related project conventions or future pipeline files.

### `scripts/check.sh`

Use as the entry point for lightweight validation steps.

### `scripts/test.sh`

Use as the entry point for project tests.

### `scripts/build.sh`

Use as the entry point for project build steps.

## File philosophy

- keep everything minimal
- avoid framework lock-in
- prefer placeholders and clear TODOs over fake completeness
- do not generate Docker or deployment files here
