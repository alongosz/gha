# Semantic Release

A composite action that runs semantic-release with Node.js setup and configurable options.

## Inputs

| Name | Description | Required | Default |
|------|-------------|----------|---------|
| `node-version` | Node.js version to use | No | `18` |
| `working-directory` | Working directory for semantic-release | No | `.` |
| `dry-run` | Run semantic-release in dry-run mode | No | `false` |
| `extends` | Shareable configuration to extend | No | `` |
| `branches` | Branches configuration (JSON format) | No | `` |
| `plugins` | Additional plugins to install (space-separated) | No | `` |

## Outputs

| Name | Description |
|------|-------------|
| `published` | Whether a new release was published |
| `version` | The version of the new release |
| `release-notes` | The release notes of the new release |

## Usage

```yaml
- name: Run semantic release
  uses: alongosz/gha/actions/semantic-release@main
  env:
    GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
    NPM_TOKEN: ${{ secrets.NPM_TOKEN }}
```

## Examples

### Basic usage
```yaml
- uses: alongosz/gha/actions/semantic-release@main
  env:
    GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

### Dry run mode
```yaml
- uses: alongosz/gha/actions/semantic-release@main
  with:
    dry-run: 'true'
  env:
    GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

### With custom configuration
```yaml
- uses: alongosz/gha/actions/semantic-release@main
  with:
    extends: '@semantic-release/config-conventional'
    plugins: '@semantic-release/changelog @semantic-release/git'
  env:
    GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
    NPM_TOKEN: ${{ secrets.NPM_TOKEN }}
```

### Custom branches configuration
```yaml
- uses: alongosz/gha/actions/semantic-release@main
  with:
    branches: |
      [
        "main",
        {"name": "beta", "prerelease": true},
        {"name": "alpha", "prerelease": true}
      ]
  env:
    GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

### Different Node.js version and working directory
```yaml
- uses: alongosz/gha/actions/semantic-release@main
  with:
    node-version: '20'
    working-directory: './packages/core'
  env:
    GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```