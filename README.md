# cr-semantic-release

A [common-repo](https://github.com/common-repo/common-repo) source template for conventional commits and semantic releases.

## What's Included

Files distributed from `src/`:

| File | Purpose |
|---|---|
| `.releaserc.yaml` | semantic-release config (conventionalcommits preset, changelog, git, GitHub release, major-tag) |
| `commitlint.config.js` | commitlint config extending `@commitlint/config-conventional` |
| `.github/workflows/commitlint.yml` | PR commit lint workflow using `wagoid/commitlint-github-action` |
| `.github/workflows/release.yaml` | Semantic release workflow (triggers on push to main, uses GitHub App token) |

## Usage

### Add to an existing `.common-repo.yaml`

```yaml
# .common-repo.yaml
- repo:
    url: https://github.com/christmas-island/cr-semantic-release
    ref: v1.0.0
    with:
      - include: ["src/**", "src/.*", "src/.*/**"]
      - rename:
          - "^src/(.*)$": "$1"
```

> **Note:** Source-declared filtering is not yet functional in common-repo 0.27.0
> ([#226](https://github.com/common-repo/common-repo/issues/226),
> [#227](https://github.com/common-repo/common-repo/issues/227)).
> The `with:` clause above is required until those are fixed, at which point
> consumers will only need the `repo:` block.

### Apply

```bash
cr diff    # preview changes
cr apply   # apply
```

## Repo Structure

```
cr-semantic-release/
├── .github/workflows/     ← this repo's own CI (dogfooding)
│   ├── ci.yaml            ← sync check: top-level == src/
│   ├── commitlint.yml     ← commit linting for this repo
│   └── release.yaml       ← semantic release for this repo
├── .releaserc.yaml        ← this repo's own release config
├── commitlint.config.js   ← this repo's own commitlint
├── README.md
├── LICENSE
└── src/                   ← distributed to consumers
    ├── .github/workflows/
    │   ├── commitlint.yml
    │   └── release.yaml
    ├── .releaserc.yaml
    └── commitlint.config.js
```

The top-level files and `src/` files are identical — the repo eats its own dog food. CI enforces they stay in sync.

## Prerequisites

The release workflow expects the following GitHub org-level vars and secrets:

| Name | Type | Purpose |
|---|---|---|
| `CHRISTMAS_ISLAND_APP_ID` | Variable | GitHub App ID for generating tokens |
| `CHRISTMAS_ISLAND_PRIVATE_KEY` | Secret | GitHub App private key |

These are used by `actions/create-github-app-token` to generate a token with write permissions for creating releases and pushing tags/changelogs.

## Customization

### Release workflow

The included `release.yaml` contains only the semantic-release job. It does **not** include a publish step (goreleaser, Docker, etc.) — add that in your repo's own workflow or extend via common-repo merge operators.

The workflow calls `./.github/workflows/ci.yaml` as a prerequisite. Your repo must have a CI workflow at that path (or remove the `ci` job dependency).

### Excluding files

If you only want a subset:

```yaml
- repo:
    url: https://github.com/christmas-island/cr-semantic-release
    ref: v1.0.0
    with:
      - include: ["src/.releaserc.yaml", "src/commitlint.config.js"]
      - rename:
          - "^src/(.*)$": "$1"
```

### Overriding `.releaserc.yaml`

Use common-repo's YAML merge operator to patch specific fields:

```yaml
- repo:
    url: https://github.com/christmas-island/cr-semantic-release
    ref: v1.0.0
    with:
      - include: ["src/**", "src/.*", "src/.*/**"]
      - rename:
          - "^src/(.*)$": "$1"
- yaml:
    source: my-releaserc-overrides.yaml
    dest: .releaserc.yaml
    path: plugins
    array_mode: replace
```
