# Docker Build and Push

A composite action that builds Docker images and pushes them to a registry with caching support.

## Inputs

| Name | Description | Required | Default |
|------|-------------|----------|---------|
| `image-name` | Docker image name | Yes | - |
| `registry` | Docker registry (e.g., docker.io, ghcr.io) | No | `docker.io` |
| `username` | Registry username | Yes | - |
| `password` | Registry password or token | Yes | - |
| `dockerfile` | Path to Dockerfile | No | `./Dockerfile` |
| `context` | Build context path | No | `.` |
| `platforms` | Target platforms for build (comma-separated) | No | `linux/amd64` |
| `push` | Push image to registry | No | `true` |
| `tags` | Additional tags (comma-separated) | No | `` |

## Outputs

| Name | Description |
|------|-------------|
| `image-digest` | Image digest |
| `image-metadata` | Image metadata |

## Usage

```yaml
- name: Build and push Docker image
  uses: alongosz/gha/actions/docker-build-push@main
  with:
    image-name: myapp
    registry: ghcr.io
    username: ${{ github.actor }}
    password: ${{ secrets.GITHUB_TOKEN }}
```

## Examples

### Basic usage with Docker Hub
```yaml
- uses: alongosz/gha/actions/docker-build-push@main
  with:
    image-name: myusername/myapp
    username: ${{ secrets.DOCKER_USERNAME }}
    password: ${{ secrets.DOCKER_PASSWORD }}
```

### GitHub Container Registry
```yaml
- uses: alongosz/gha/actions/docker-build-push@main
  with:
    image-name: myapp
    registry: ghcr.io
    username: ${{ github.actor }}
    password: ${{ secrets.GITHUB_TOKEN }}
```

### Multi-platform build with custom tags
```yaml
- uses: alongosz/gha/actions/docker-build-push@main
  with:
    image-name: myapp
    registry: ghcr.io
    username: ${{ github.actor }}
    password: ${{ secrets.GITHUB_TOKEN }}
    platforms: linux/amd64,linux/arm64
    tags: |
      type=raw,value=latest
      type=raw,value=v1.0.0
```

### Custom Dockerfile and context
```yaml
- uses: alongosz/gha/actions/docker-build-push@main
  with:
    image-name: myapp
    username: ${{ secrets.DOCKER_USERNAME }}
    password: ${{ secrets.DOCKER_PASSWORD }}
    dockerfile: ./docker/Dockerfile.prod
    context: ./app
```