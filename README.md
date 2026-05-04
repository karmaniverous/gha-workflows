# gha-workflows

Reusable GitHub Actions workflows.

## Workflows

### npm-pack-check

Runs `npm pack --dry-run` for every publishable package in the repo and fails
if any tarball would include files matching a forbidden pattern. Handles
single-package repos and npm/pnpm workspaces automatically.

**Usage:**

```yaml
name: Pack Check

on:
  pull_request:
  push:
    branches: [main]

jobs:
  pack-check:
    uses: karmaniverous/gha-workflows/.github/workflows/npm-pack-check.yml@main
```

**Inputs (all optional):**

| Input | Default | Description |
| --- | --- | --- |
| `forbidden-patterns` | `*.local` | Pipe-separated globs to reject |
| `node-version` | `22` | Node.js version |
| `install-command` | `npm ci` | Dependency install command |

**Example with custom patterns:**

```yaml
jobs:
  pack-check:
    uses: karmaniverous/gha-workflows/.github/workflows/npm-pack-check.yml@main
    with:
      forbidden-patterns: '*.local|*.pem|*.key'
```

### cloud-sync

Syncs files using rclone. Requires `RCLONE_CONFIG` secret.

### docs

Deploys documentation.

### jekyll-deploy

Deploys Jekyll sites to GitHub Pages.

### linux-compat

Tests build and test across multiple Node.js versions on Linux.

### sync

Triggers cloud-sync workflow.
