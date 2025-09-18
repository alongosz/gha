# GitHub Actions Repository

A collection of reusable GitHub composite actions for common CI/CD workflows.

## Available Actions

### 🚀 [Setup Node.js with Cache](./actions/setup-node-cache)
Sets up Node.js with the specified version and enables dependency caching for npm, yarn, or pnpm.

```yaml
- uses: alongosz/gha/actions/setup-node-cache@main
  with:
    node-version: '18'
    cache: 'npm'
```

### 🐳 [Docker Build and Push](./actions/docker-build-push)
Builds Docker images and pushes them to a registry with caching support and multi-platform builds.

```yaml
- uses: alongosz/gha/actions/docker-build-push@main
  with:
    image-name: myapp
    registry: ghcr.io
    username: ${{ github.actor }}
    password: ${{ secrets.GITHUB_TOKEN }}
```

### 📦 [Semantic Release](./actions/semantic-release)
Runs semantic-release with Node.js setup and configurable options for automated versioning and publishing.

```yaml
- uses: alongosz/gha/actions/semantic-release@main
  env:
    GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
    NPM_TOKEN: ${{ secrets.NPM_TOKEN }}
```

## Repository Structure

```
actions/
├── setup-node-cache/       # Node.js setup with caching
│   ├── action.yml           # Action definition
│   └── README.md           # Action documentation
├── docker-build-push/      # Docker build and push
│   ├── action.yml
│   └── README.md
└── semantic-release/       # Semantic release automation
    ├── action.yml
    └── README.md
```

## Usage

To use any of these actions in your workflow, reference them using the following syntax:

```yaml
- uses: alongosz/gha/actions/<action-name>@<version>
```

Where:
- `<action-name>` is the directory name of the action (e.g., `setup-node-cache`)
- `<version>` is the git reference (e.g., `main`, `v1.0.0`, commit SHA)

### Examples

```yaml
name: CI
on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Setup Node.js
        uses: alongosz/gha/actions/setup-node-cache@main
        with:
          node-version: '18'
          cache: 'npm'
      
      - name: Run tests
        run: npm test
      
      - name: Build and push Docker image
        uses: alongosz/gha/actions/docker-build-push@main
        with:
          image-name: myapp
          registry: ghcr.io
          username: ${{ github.actor }}
          password: ${{ secrets.GITHUB_TOKEN }}
        if: github.event_name == 'push' && github.ref == 'refs/heads/main'
```

## Contributing

When adding a new action:

1. Create a new directory under `actions/` with a descriptive name
2. Add an `action.yml` file with the action definition
3. Add a `README.md` file with documentation and examples
4. Update this main README.md to include the new action
5. Follow the existing patterns for inputs, outputs, and documentation

### Action Template

```yaml
name: 'Action Name'
description: 'Action description'
author: 'Andrew Longosz'

inputs:
  input-name:
    description: 'Input description'
    required: false
    default: 'default-value'

outputs:
  output-name:
    description: 'Output description'
    value: ${{ steps.step-id.outputs.value }}

runs:
  using: 'composite'
  steps:
    - name: Step name
      id: step-id
      shell: bash
      run: |
        echo "Hello from composite action!"
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
