# Nushell plugin

[Nushell](https://www.nushell.sh/) WASM plugin for [proto](https://moonrepo.dev/proto).

This plugin installs the official prebuilt Nushell release archives from
[`nushell/nushell`](https://github.com/nushell/nushell/releases).

## Installation

Add the following to `.prototools`:

```toml
[plugins]
nu = "github://hebilicious/proto-nu"

[tools.nu]
version = "0.112.2"
```

Or add it explicitly:

```shell
proto plugin add nu github://hebilicious/proto-nu
```

## Usage

```shell
# install latest stable release
proto install nu

# install a specific version
proto install nu 0.112.2

# run Nushell
proto run nu -- --version
proto run nu -- -c 'version | get version'
```

## Version Detection

The plugin checks version files in this order:

1. `.nu-version`
2. `.nushell-version`

Supported formats:

```text
0.112.2
nu-0.112.2
stable
```

## Supported Platforms

- Linux x64, glibc and musl
- Linux arm64, glibc and musl
- macOS x64
- macOS arm64
- Windows x64
- Windows arm64

## Notes

- Nushell release archives include several `nu_plugin_*` binaries. The plugin
  exposes these binaries through proto alongside the primary `nu` executable.
- Windows installs use the release `.zip` archive, not the `.msi` installer.

## Contributing

```shell
rustup target add wasm32-wasip1
cargo build --target wasm32-wasip1
cargo test
./tests/e2e/run.sh
```

## Releases

This repository uses [`release-plz`](https://release-plz.dev/) to manage
version bumps and release pull requests.

Merging changes into `main` updates or creates the automated release PR.
Merging that release PR creates the version tag, and the same `main` workflow
publishes the GitHub release artifact for that tag.
