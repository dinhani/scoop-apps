# scoop-dinhani

Personal [Scoop](https://scoop.sh) bucket for apps that aren't available in the official buckets.

## Usage

```powershell
scoop bucket add dinhani https://github.com/dinhani/scoop-dinhani
scoop install dinhani/<app>
```

## Adding an app

Drop a `<app>.json` manifest into `bucket/`. Minimal shape:

```json
{
    "version": "1.0.0",
    "description": "What the app does",
    "homepage": "https://example.com",
    "license": "MIT",
    "url": "https://example.com/app-1.0.0.zip",
    "hash": "sha256-of-the-file",
    "bin": "app.exe",
    "checkver": "github",
    "autoupdate": {
        "url": "https://github.com/owner/repo/releases/download/v$version/app-$version.zip"
    }
}
```

See `bucket/_template.json` for a fuller example and the
[manifest reference](https://github.com/ScoopInstaller/Scoop/wiki/App-Manifests).

Get a file hash with:

```powershell
(Get-FileHash -Algorithm SHA256 .\app.zip).Hash.ToLower()
```
