# jinnangxia

Official binary distribution of jinnangxia by 亮有一计.

Website: https://liangyouyiji.com · Support: support@liangyouyiji.com

This repository contains installation tooling and binary releases. Application source code is maintained privately. GitHub's automatically generated “Source code” archives contain only this distribution repository; download the platform archive to install jinnangxia.

## Install

Install [Cosign](https://docs.sigstore.dev/cosign/system_config/installation/) first (the release verification flow uses Cosign 2.6.0). Then download and inspect the installer:

```sh
curl -fsSLO https://raw.githubusercontent.com/liangyouyiji-dev/jinnangxia/main/scripts/install.sh
bash install.sh
```

Default installation path: `~/.local/bin/jinnangxia`. Add `~/.local/bin` to your PATH if needed. Use `--install-dir PATH` or `--no-skill` to customize installation. Windows users can download the matching ZIP from Releases and verify it before extracting `jinnangxia.exe`.

## Releases and verification

Download your platform archive from [GitHub Releases](https://github.com/liangyouyiji-dev/jinnangxia/releases/latest).

Releases include macOS (amd64/arm64), Linux (amd64/arm64/386/riscv64), and Windows (amd64/arm64) archives, a dependency SBOM, SHA-256 checksums, and Cosign signature/certificate files. Distribution checksums are signed by this repository's `.github/workflows/release.yml` workflow at the release tag, using GitHub Actions OIDC. This authenticates the distribution; it is not a claim that private application source was built on GitHub.

Prereleases are staging candidates. Use a stable release with its complete signature files. The installer verifies publisher identity, checksum, version and command contracts before installation. macOS executables are not Apple-notarized; follow your organization's software approval process if Gatekeeper intervenes.

## Version and upgrade

```sh
jinnangxia version
jinnangxia upgrade --check
jinnangxia upgrade
```

Upgrade checks the latest stable GitHub release and only upgrades when it is newer. `jinnangxia upgrade --force` explicitly reinstalls the latest release (including a downgrade). `jinnangxia upgrade --no-skill` updates only the executable. Cosign must be available on PATH. The previous executable is retained as `jinnangxia.bak`. Configure and log into your own endpoint with an explicit `--profile local|test|prod`; installation does not configure production access.

Version checks and upgrades are independent of backend profiles and login credentials. They work even when a production endpoint is not configured. Set their output preferences with command-line flags or `JINNANGXIA_FORMAT` / `JINNANGXIA_LANG`.

For bugs or installation questions, open an issue without credentials, tokens or personal data.

## Migration from flowctl

The product is now 锦囊匣. Install `jinnangxia` from this repository and update scripts and Agent instructions to use the new command and `$jinnangxia` Skill. Environment variables now use `JINNANGXIA_`; the default configuration directory is `~/.jinnangxia`. The installer does not copy credentials or read the old directory automatically. To deliberately reuse your own previous configuration, set `JINNANGXIA_CONFIG_DIR` to its absolute directory and check your endpoint and profile before running commands. Historical flowctl downloads remain in the old distribution repository; its upgrade command does not migrate across repositories.
