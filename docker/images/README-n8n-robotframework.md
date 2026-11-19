# n8n Robot Framework Docker Images

This builds the complete n8n Robot Framework Docker image stack.

## Why Debian Bookworm?

These images use **Debian Bookworm** instead of Alpine Linux. The key reason is that Robot Framework Browser (Playwright) requires **glibc**, which Debian provides. Alpine uses **musl libc**, which is incompatible with Playwright's pre-built binaries.

## Build Options

### Option 1: GitHub Actions (Recommended for multi-platform)

Builds and pushes AMD64 + ARM64 images to Docker Hub automatically.

1. Go to **Actions** → **Build n8n Robot Framework Images**
2. Click **Run workflow**
3. Optionally enter versions; empty fields use the defaults from [versions.env](../../versions.env)
4. Images are pushed to Docker Hub

**Required secrets:**
- `DOCKERHUB_TOKEN` - Docker Hub access token

### Option 2: Local Build (Single platform)

Builds for your host architecture only.

**Prerequisites:**
- Docker installed and running
- Run from the project root directory

**Usage:**

```bash
./docker/images/build-n8n-robotframework.sh [NAME=VERSION ...]
```

### Parameters

Default versions are defined in [versions.env](../../versions.env), the single place to change them. Any of them can be overridden per build as `NAME=VERSION`.

| Parameter | Description |
|-----------|-------------|
| `NODE_VERSION` | Node.js version for the base image |
| `N8N_VERSION` | n8n version |
| `ROBOTFRAMEWORK_VERSION` | Robot Framework version |
| `RF_BROWSER_VERSION` | robotframework-browser version |
| `RF_ASSERTION_ENGINE_VERSION` | robotframework-assertion-engine version (must match what robotframework-browser requires) |
| `RF_JSONLIBRARY_VERSION` | robotframework-jsonlibrary version |

### Example

```bash
./docker/images/build-n8n-robotframework.sh
./docker/images/build-n8n-robotframework.sh N8N_VERSION=2.48.6 RF_BROWSER_VERSION=21.0.0
```

## Images Built

The script builds 3 images in sequence:

1. **n8n_base** - Base image with Node.js and system dependencies
   - `delilovic/n8n_base:<NODE_VERSION>-bookworm-slim`

2. **n8n** - Main n8n application (installed from npm)
   - `delilovic/n8n:<N8N_VERSION>-bookworm-slim`
   - `delilovic/n8n:latest`

3. **n8n_robotframework** - n8n with Robot Framework and Playwright
   - `delilovic/n8n_robotframework:<N8N_VERSION>-bookworm-slim`
   - `delilovic/n8n_robotframework:latest`
