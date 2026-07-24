# Branching and Git Workflow

**Last verified:** 2026-07-24

---

## Overview

Club OS uses a trunk-based development model with short-lived feature branches.

---

## Branch Types

| Branch type | Pattern | Purpose |
|---|---|---|
| Main | `main` | Production-ready code. Protected. |
| Feature | `feature/{ticket-id}-{description}` | New features and enhancements |
| Fix | `fix/{ticket-id}-{description}` | Bug fixes |
| Hotfix | `hotfix/{version}-{description}` | Emergency production fixes |
| Release | `release/{version}` | Release preparation |
| Docs | `docs/{description}` | Documentation-only changes |

---

## Branch Rules

- `main` is protected. Direct pushes are not permitted.
- All changes to `main` go through a pull request with at least one approval.
- Feature and fix branches are created from `main` and merged back to `main`.
- Hotfix branches are created from the release tag and merged to both `main` and the release branch.
- Documentation branches (like `docs/architecture-pack`) are created from `main` and write only to the docs repository.

---

## Commit Message Convention

Club OS follows the Conventional Commits specification:

```
{type}({scope}): {description}

{optional body}

{optional footer}
```

Types: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `perf`

Scopes correspond to module names: `finance`, `people`, `portal`, `permissions`, `communications`, `match-mode`, etc.

Examples:

```
feat(finance): add bulk invoice creation endpoint
fix(portal): resolve coach workspace redirect loop
docs(architecture): add database table reference
chore(deps): update composer dependencies
```

---

## Pull Request Process

1. Create a pull request from your feature branch to `main`
2. Fill in the pull request template
3. Ensure all CI checks pass
4. Request review from at least one team member
5. Address all review comments
6. Merge using **Squash and Merge** to keep `main` history clean

---

## Release Process

See [RELEASE_CHECKLIST.md](RELEASE_CHECKLIST.md) for the full release process.

---

## Documentation Repository

The documentation repository (`iexel-club-os-docs`) uses the same branching conventions. The `docs/architecture-pack` branch contains the Architecture Pack documentation. Documentation branches are never merged to `main` automatically; they are reviewed and merged separately.
