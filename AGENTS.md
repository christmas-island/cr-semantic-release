# cr-semantic-release

common-repo source template that ships conventional-commit + semantic-release tooling to consumers. The repo dogfoods its own `src/` payload at top level.

## Layout

- `src/` — distributed payload (`.releaserc.yaml`, `commitlint.config.js`, `.github/workflows/{commitlint,release}.yaml`) — renamed to consumer root by `.common-repo.yaml`
- `.github/workflows/` — this repo's own CI (lint, config validation, dogfood commitlint/release, sync check)
- `.common-repo.yaml` — source-declared filtering + template variables (`GH_APP_ID_VAR`, `GH_APP_KEY_SECRET`, `GH_APP_OWNER`)
- `cog.toml` — cocogitto config (`tag_prefix = "v"`, ignore merge commits)

## Required

- Top-level files must stay identical to `src/` counterparts, **except** `src/.github/workflows/release.yaml` which carries template variables while the top-level copy uses hardcoded defaults. CI (`ci.yaml`) enforces the sync.
- Conventional commits are mandatory (`commitlint.yml` on PRs). Release is semantic-release on push to `main` via a GitHub App token.
- pre-commit hooks: trailing whitespace, EOF, YAML check, merge-conflict check, large-file check.
- Consumers need **common-repo ≥ 0.28.4** (source-declared filtering + template var overrides).

## Commands

```bash
pre-commit run --all-files
common-repo validate
common-repo apply --dry-run
```

Consumer apply: add the repo to `.common-repo.yaml`, then `cr diff` / `cr apply`.

## Key libraries

- [common-repo](https://github.com/common-repo/common-repo) — config-as-dependency apply
- cocogitto (`cog`) — versioning/changelog
- semantic-release + `@commitlint/config-conventional` + `wagoid/commitlint-github-action`

## Maintaining this index

- Update the affected `AGENTS.md` files in the same change when paths,
  responsibilities, commands, dependencies, or conventions change.
- Keep indexes brief: record semantic entry points and non-obvious
  constraints; link to existing documentation instead of duplicating it.
- Add a directory index only when it provides useful navigation beyond its
  parent; omit generated, vendored, and fixture trees.
- Do not add `CLAUDE.md` files; Claude Code reads `AGENTS.md` natively, and
  a `CLAUDE.md` anywhere in the tree stops every `AGENTS.md` from loading.

