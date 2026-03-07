# Dakota Studio — Releases

This repository hosts auto-update artifacts for [Dakota Studio](https://github.com/DakotaDataEng/dakota-studio), an internal desktop app by Dakota Analytics for agentic engineering.

## About Dakota Studio

Dakota Studio is a Tauri 2 desktop app (Rust backend + React frontend) for running Claude Code across multiple projects and tasks, each in isolated git worktrees. Key features include:

- **Multi-task workspace** — Run multiple Claude Code sessions simultaneously, each in its own git worktree for full isolation
- **Integrated terminal** — Built-in PTY terminals with activity monitoring, prompt detection, and session snapshots
- **Git operations** — Visual commit graph, branch management, staging, diffing, and AI-generated commit messages
- **File explorer & editor** — Monaco-based code editor with search/replace, preview tabs, and live file watching
- **GitHub integration** — Issue linking, creation, and search directly from the app
- **Conversation search** — Full-text search across Claude Code conversations with FTS5 indexing
- **Auto-updates** — Signed update bundles delivered through this repo (see below)
- **Offline-first** — All assets bundled locally, no CDN dependencies at runtime
- **Cross-platform** — Windows (NSIS) and Linux (AppImage) builds

## How updates work

Dakota Studio uses [Tauri's built-in updater](https://v2.tauri.app/plugin/updater/) to check for new versions on launch. This public repo serves as the update endpoint — the app fetches `latest.json` from the most recent GitHub Release to determine if an update is available.

**Update flow:**
1. App launches and checks `latest.json` from this repo's latest release
2. If a newer version exists, the user is prompted to install
3. The signed installer is downloaded and verified against the bundled public key
4. App restarts with the new version

## Release artifacts

Each release contains:

| File | Purpose |
|------|---------|
| `latest.json` | Tauri updater manifest (version, platform URLs, signatures) |
| `*.nsis.zip` | Windows installer bundle |
| `*.nsis.zip.sig` | Windows installer Ed25519 signature |
| `*.AppImage` | Linux installer |
| `*.AppImage.sig` | Linux installer Ed25519 signature |

## Security

All update bundles are signed with an Ed25519 key. The app verifies the signature before applying any update — tampered artifacts are rejected.

## Source code

The application source code lives in the private [DakotaDataEng/dakota-studio](https://github.com/DakotaDataEng/dakota-studio) repository. This repo contains only release artifacts.
