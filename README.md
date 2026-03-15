# cr-semantic-release

A [common-repo](https://github.com/common-repo/common-repo) source template for conventional commits and semantic releases.

## What's Included

| File | Purpose |
|---|---|
| `.releaserc.yaml` | semantic-release config (conventionalcommits preset, changelog, git, GitHub release, major-tag) |
| `commitlint.config.js` | commitlint config extending `@commitlint/config-conventional` |
| `.github/workflows/commitlint.yml` | PR commit lint workflow using `wagoid/commitlint-github-action` |
| `.github/workflows/release.yaml` | Semantic release workflow (triggers on push to main, uses GitHub App token) |

## Usage

### Add to a new repo

```bash
cr init https://github.com/christmas-island/cr-semantic-release
```

### Add to an existing `.common-repo.yaml`

```bash
cr add https://github.com/christmas-island/cr-semantic-release
```

Or manually:

```yaml
# .common-repo.yaml
- repo:
    url: https://github.com/christmas-island/cr-semantic-release
    ref: v1.0.0
```

### Apply

```bash
cr diff    # preview changes
cr apply   # apply
```

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

If you only want a subset of files:

```yaml
- repo:
    url: https://github.com/christmas-island/cr-semantic-release
    ref: v1.0.0
    with:
      - exclude: [".github/workflows/commitlint.yml"]
```

### Overriding `.releaserc.yaml`

Use common-repo's YAML merge operator to patch specific fields:

```yaml
- repo:
    url: https://github.com/christmas-island/cr-semantic-release
    ref: v1.0.0
- yaml:
    source: my-releaserc-overrides.yaml
    dest: .releaserc.yaml
    path: plugins
    array_mode: replace
```
