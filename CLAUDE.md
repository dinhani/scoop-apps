# scoop-dinhani

Personal [Scoop](https://scoop.sh) bucket for Windows apps not available in any official or community bucket. **For my own use only** — not meant to be a general-purpose or widely-published bucket, so don't optimize for other consumers, broad compatibility, or polished docs. If an app already exists in a known bucket, it doesn't belong here.

## Layout

- `bucket/*.json` — one manifest per app. This is the entire bucket; Scoop reads every `*.json` here.
- `bucket/_template.json` — copy this as the starting point for a new manifest (the leading `_` keeps it out of `scoop install` listings).
- `.github/workflows/excavator.yml` — Scoop's Excavator runs every 6h, follows `checkver`/`autoupdate`, and auto-commits version bumps. Don't hand-edit `version`/`hash` for apps that autoupdate — let Excavator do it.

## Adding an app

1. Copy `_template.json` to `bucket/<app>.json` (lowercase, the filename is the install name).
2. Fill `version`, `description`, `homepage`, `license`, `url`/`hash` (or per-arch `architecture`).
3. Wire up `checkver` + `autoupdate` so Excavator keeps it current. Skip only if upstream has no stable version source.
4. Validate: `scoop install dinhani/<app>` locally before committing.

Get a hash: `(Get-FileHash -Algorithm SHA256 .\app.zip).Hash.ToLower()`

## Conventions

- Manifests are JSON, 4-space indent, matching `_template.json`.
- Prefer GitHub releases as the source (`checkver: { "github": ... }`) — it's the most reliable path for autoupdate.
- Conventional Commits, e.g. `feat(app): add <name>`, `chore(app): bump <name>`.
- The `.gitignore` excludes downloaded binaries (`*.zip`, `*.exe`, etc.) — never commit the actual app payloads, only manifests.
