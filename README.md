# neoclaw-release

Download artifacts for [neoclaw](https://neosoul.ai/) — a self-custodial
trading agent runtime for prediction markets.

This repository holds published artifacts only. Source lives elsewhere.

> **Development preview.** Everything published so far is a `-dev.N`
> pre-release built from a branch snapshot, not a stable version. The desktop
> app is **not notarized (macOS) and not code-signed (Windows)** — both systems
> will warn that it comes from an unidentified developer. Do not use with real
> funds.

## Install the desktop app

Latest: [`v0.1.0-dev.1`](../../releases/tag/v0.1.0-dev.1) — see the release
notes there for per-file checksums and the full install steps.

| Platform | Download |
| --- | --- |
| macOS (Apple Silicon) | [`neoclaw_0.1.0_aarch64.dmg`](../../releases/download/v0.1.0-dev.1/neoclaw_0.1.0_aarch64.dmg) |
| macOS (Intel) | [`neoclaw_0.1.0_x64.dmg`](../../releases/download/v0.1.0-dev.1/neoclaw_0.1.0_x64.dmg) |
| Windows x64 | [`neoclaw_0.1.0_x64-setup.exe`](../../releases/download/v0.1.0-dev.1/neoclaw_0.1.0_x64-setup.exe) · [`.msi`](../../releases/download/v0.1.0-dev.1/neoclaw_0.1.0_x64_en-US.msi) |
| Linux x86_64 | [`.deb`](../../releases/download/v0.1.0-dev.1/neoclaw_0.1.0_amd64.deb) · [`.rpm`](../../releases/download/v0.1.0-dev.1/neoclaw-0.1.0-1.x86_64.rpm) · [`.AppImage`](../../releases/download/v0.1.0-dev.1/neoclaw_0.1.0_amd64.AppImage) |

### macOS

    curl -fLO https://github.com/NeoSoul-AI/neoclaw-release/releases/download/v0.1.0-dev.1/neoclaw_0.1.0_aarch64.dmg
    shasum -a 256 neoclaw_0.1.0_aarch64.dmg
    # 29e7a7ad666039e8c6165183d4f5bdb9631ec12fa989c0cd0ec7fc3c3c3e1c0e
    open neoclaw_0.1.0_aarch64.dmg      # drag neoclaw.app into Applications
    xattr -dr com.apple.quarantine /Applications/neoclaw.app

Without the `xattr` step macOS reports *"neoclaw is damaged and can't be
opened"*. The app is not damaged — that is Gatekeeper's message for an
un-notarized bundle.

### Windows

In PowerShell, `curl` is an alias for `Invoke-WebRequest`; call `curl.exe`:

    curl.exe -fLO https://github.com/NeoSoul-AI/neoclaw-release/releases/download/v0.1.0-dev.1/neoclaw_0.1.0_x64-setup.exe
    Get-FileHash .\neoclaw_0.1.0_x64-setup.exe -Algorithm SHA256
    # 2FEEAF92545BA6DD8FD5794B575763792BDC4373C2D6D65FA5BD63F970395088

SmartScreen blocks the unsigned installer: **More info** → **Run anyway**.

### Linux

    curl -fLO https://github.com/NeoSoul-AI/neoclaw-release/releases/download/v0.1.0-dev.1/neoclaw_0.1.0_amd64.deb
    sha256sum neoclaw_0.1.0_amd64.deb
    # e20d8a742ad97b0db2ac838641ed6fc3f37c26c862ae7979c9ca5a7af2e442c8
    sudo dpkg -i neoclaw_0.1.0_amd64.deb && sudo apt-get -f install

## Install the CLI

Requires Node >= 24.

    curl -fLO https://github.com/NeoSoul-AI/neoclaw-release/releases/download/v0.1.0-dev.1/neoclaw-0.1.0.tgz
    npm i -g ./neoclaw-0.1.0.tgz
    neoclaw status

Verify the download before installing:

    shasum -a 256 neoclaw-0.1.0.tgz
    # a73b06c34a630794fcba10b3b3c8c1e7663887c2b00b3d25129f6597de8a7e6a

## Releases

See [Releases](../../releases). Pre-release tags (`-dev.N`) are development
builds, not stable versions. The desktop app and the CLI within one release may
be built from different source commits — each release's notes state which.
