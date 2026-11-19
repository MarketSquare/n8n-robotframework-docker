# n8n Robot Framework Docker

Docker images for n8n with Robot Framework and Playwright support.

## Images

| Image | Description |
|-------|-------------|
| `delilovic/n8n_base` | Base image with Node.js and system dependencies |
| `delilovic/n8n` | n8n workflow automation (installed from npm) |
| `delilovic/n8n_robotframework` | n8n with Robot Framework and Playwright |

## Why Debian Bookworm?

These images use **Debian Bookworm** instead of Alpine Linux because Robot Framework Browser (Playwright) requires **glibc**. Alpine uses musl libc, which is incompatible with Playwright's pre-built binaries.

## Build

### GitHub Actions (Multi-platform: AMD64 + ARM64)

1. Go to **Actions** → **Build n8n Robot Framework Images**
2. Click **Run workflow**
3. Adjust the versions if needed (defaults are prefilled)
4. Images are pushed to Docker Hub

### Local Build (Host architecture only)

```bash
./docker/images/build-n8n-robotframework.sh [NAME=VERSION ...]
```

Default versions come from the workflow inputs in [build-n8n-robotframework.yml](.github/workflows/build-n8n-robotframework.yml), the single place to change them. Any of them can be overridden as `NAME=VERSION`:
```bash
./docker/images/build-n8n-robotframework.sh
./docker/images/build-n8n-robotframework.sh N8N_VERSION=2.48.6 RF_BROWSER_VERSION=21.0.0
```

## Run

```bash
docker run -it --rm --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  delilovic/n8n_robotframework:latest
```

## Requirements

- Docker
- Docker Hub account (for pushing images)
- `DOCKERHUB_TOKEN` secret in GitHub (for Actions)

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for what changed in each release.
