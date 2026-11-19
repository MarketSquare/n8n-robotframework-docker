# Changelog

All notable changes to this project are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
Each change gets a new section at the top, named by date and n8n version (the n8n version matches the Docker image tag).

## 2026-11-19 — n8n 2.48.6

### Added
- GitHub Actions inputs for the Robot Framework, Browser, assertion-engine and JSONLibrary versions. The input defaults in the workflow are the single place for all default versions; the local build script reads them from there.
- Build script accepts `NAME=VERSION` overrides for every version.
- `MAGICK_CODER_STABILITY=PRIMARY` from the upstream n8n image, restricting GraphicsMagick to its commonly used coders.

### Changed
- Node.js 22.22.0 → 24.22.2 and n8n 2.4.4 → 2.48.6. n8n 2.48.6 requires Node.js >= 24; 24.22.2 is one of the upstream n8n base images. Node.js 26 is not used yet because @confluentinc/kafka-javascript has no prebuilt binary for it and does not compile against the Debian Bookworm librdkafka.
- Robot Framework 7.4.1 → 7.5.1, robotframework-browser 19.12.4 → 21.0.0, robotframework-assertion-engine 3.1.3 → 5.0.1.
- Build script no longer takes positional arguments; versions come from the workflow input defaults or `NAME=VERSION` overrides.
- Base image sets `NODE_PATH=/usr/local/lib/node_modules` instead of `NODE_ICU_DATA`, as upstream does.
- n8n image build fails on errors instead of ignoring them (`set -e` instead of `|| true`).

### Removed
- Global npm packages `weaviate-client`, `@mozilla/readability` and `@postlight/parser` from the n8n-robotframework image.
- `full-icu` from the base image (Node.js ships with full ICU).

## 2026-02-11

### Changed
- robotframework-browser bumped to 19.12.4.

### Fixed
- Missing robotframework-assertion-engine dependency.

## 2026-01-25

### Added
- n8n Robot Framework Docker images (n8n_base, n8n, n8n_robotframework) on Debian Bookworm, with GitHub Actions workflow and local build script.
- docker-compose example for server deployment with Caddy.
