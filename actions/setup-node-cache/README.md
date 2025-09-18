# Setup Node.js with Cache

A composite action that sets up Node.js with the specified version and enables dependency caching.

## Inputs

| Name | Description | Required | Default |
|------|-------------|----------|---------|
| `node-version` | Node.js version to setup | No | `18` |
| `cache` | Enable dependency caching (npm, yarn, or pnpm) | No | `npm` |
| `working-directory` | Working directory for the action | No | `.` |

## Outputs

| Name | Description |
|------|-------------|
| `node-version` | The installed Node.js version |
| `cache-hit` | A boolean value to indicate if a cache was hit |

## Usage

```yaml
- name: Setup Node.js with caching
  uses: alongosz/gha/actions/setup-node-cache@main
  with:
    node-version: '18'
    cache: 'npm'
    working-directory: './frontend'
```

## Examples

### Basic usage with npm
```yaml
- uses: alongosz/gha/actions/setup-node-cache@main
```

### With yarn
```yaml
- uses: alongosz/gha/actions/setup-node-cache@main
  with:
    node-version: '20'
    cache: 'yarn'
```

### With pnpm and custom directory
```yaml
- uses: alongosz/gha/actions/setup-node-cache@main
  with:
    node-version: '18'
    cache: 'pnpm'
    working-directory: './app'
```