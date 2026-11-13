<p align="center">
  <img src="assets/logo.svg" alt="xorbet logo" width="128">
</p>

<h1 align="center">xorbet</h1>

<p align="center">🍧 A personal <a href="https://scoop.sh">Scoop</a> bucket. Fresh flavours, auto-updated.</p>

<p align="center">
  <a href="https://github.com/ADxorNew/xorbet/actions/workflows/ci.yml"><img src="https://github.com/ADxorNew/xorbet/actions/workflows/ci.yml/badge.svg" alt="Tests"></a>
  <a href="https://github.com/ADxorNew/xorbet/actions/workflows/excavator.yml"><img src="https://github.com/ADxorNew/xorbet/actions/workflows/excavator.yml/badge.svg" alt="Excavator"></a>
</p>

## Usage

```pwsh
scoop bucket add xorbet https://github.com/ADxorNew/xorbet
scoop install xorbet/<app>
```

Always use the `xorbet/` prefix. Some apps here also exist, with different
manifests, in other buckets.

## Flavours

| App | Description |
| --- | --- |
| [lazykeifu](https://github.com/watabegg/lazykeifu) | Graph-first Git TUI with lazygit-inspired workflows (`lzkf`) |

## How updates work

The [Excavator](.github/workflows/excavator.yml) workflow runs every 4 hours.
It reads the `checkver` block of each manifest, and when it finds a new
version it rewrites the manifest from its `autoupdate` block and commits it.

On your machine, `scoop update` pulls the bucket. `scoop status` then lists
the outdated apps, and `scoop update *` (or `scoop update <app>`) installs
them. Use `scoop hold <app>` to keep an app on its current version.

## Adding a flavour

1. Copy `bucket/app-name.json.template` to `bucket/<app>.json` and fill it in.
   Include `checkver` and `autoupdate`, so that Excavator can update it.
2. Check the manifest:

   ```pwsh
   .\bin\checkver.ps1 <app>      # shows the latest version upstream
   .\bin\checkurls.ps1 <app>     # the download URLs respond
   .\bin\checkhashes.ps1 <app>   # the hashes match the downloads
   .\bin\formatjson.ps1          # formats all manifests
   ```

3. Commit and push. The [CI](.github/workflows/ci.yml) workflow runs the
   Scoop manifest tests.

See the [App Manifests](https://github.com/ScoopInstaller/Scoop/wiki/App-Manifests)
and [App Manifest Autoupdate](https://github.com/ScoopInstaller/Scoop/wiki/App-Manifest-Autoupdate)
wiki pages for the manifest format.

## License

The bucket files are released into the public domain ([Unlicense](LICENSE)).
Each app keeps its own license, shown in its manifest.
