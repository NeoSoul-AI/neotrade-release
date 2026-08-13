# neotrade-release

Download artifacts for [NeoTrade](https://neosoul.ai/) — a self-custodial
trading agent runtime. The platform never holds your keys or your funds;
everything security-relevant runs on your own machine.

This repository holds published artifacts only. Source lives elsewhere.

> **Not notarized by Apple, not Authenticode-signed on Windows.** Every bundle
> carries an ed25519 signature verified in CI, but that is artifact integrity,
> not OS trust — so both systems warn on a first install. The two steps that
> get past them are under [Installing](#installing).

## Download

Current stable release: **[`desktop-v0.1.1`](../../releases/latest)**. The
links below name that version; the [latest release](../../releases/latest)
page always carries current ones.

**1. macOS (Apple silicon — M1/M2/M3/M4)**

Download: [`NeoTrade_0.1.1_aarch64.dmg`](../../releases/download/desktop-v0.1.1/NeoTrade_0.1.1_aarch64.dmg)

    curl -LO https://github.com/NeoSoul-AI/neotrade-release/releases/download/desktop-v0.1.1/NeoTrade_0.1.1_aarch64.dmg

**2. macOS (Intel)**

Download: [`NeoTrade_0.1.1_x64.dmg`](../../releases/download/desktop-v0.1.1/NeoTrade_0.1.1_x64.dmg)

    curl -LO https://github.com/NeoSoul-AI/neotrade-release/releases/download/desktop-v0.1.1/NeoTrade_0.1.1_x64.dmg

**3. Windows (x64, setup.exe)**

Download: [`NeoTrade_0.1.1_x64-setup.exe`](../../releases/download/desktop-v0.1.1/NeoTrade_0.1.1_x64-setup.exe)

In PowerShell, `curl` is an alias for `Invoke-WebRequest`; call `curl.exe`:

    curl.exe -LO https://github.com/NeoSoul-AI/neotrade-release/releases/download/desktop-v0.1.1/NeoTrade_0.1.1_x64-setup.exe

**4. Windows (x64, msi)**

Download: [`NeoTrade_0.1.1_x64_en-US.msi`](../../releases/download/desktop-v0.1.1/NeoTrade_0.1.1_x64_en-US.msi)

    curl.exe -LO https://github.com/NeoSoul-AI/neotrade-release/releases/download/desktop-v0.1.1/NeoTrade_0.1.1_x64_en-US.msi

**5. Linux (Debian/Ubuntu, .deb)**

Download: [`NeoTrade_0.1.1_amd64.deb`](../../releases/download/desktop-v0.1.1/NeoTrade_0.1.1_amd64.deb)

    curl -LO https://github.com/NeoSoul-AI/neotrade-release/releases/download/desktop-v0.1.1/NeoTrade_0.1.1_amd64.deb
    sudo apt install ./NeoTrade_0.1.1_amd64.deb

**6. Linux (Fedora/RHEL, .rpm)**

Download: [`NeoTrade-0.1.1-1.x86_64.rpm`](../../releases/download/desktop-v0.1.1/NeoTrade-0.1.1-1.x86_64.rpm)

    curl -LO https://github.com/NeoSoul-AI/neotrade-release/releases/download/desktop-v0.1.1/NeoTrade-0.1.1-1.x86_64.rpm
    sudo dnf install ./NeoTrade-0.1.1-1.x86_64.rpm

**7. Linux (any distro, AppImage — no install)**

Download: [`NeoTrade_0.1.1_amd64.AppImage`](../../releases/download/desktop-v0.1.1/NeoTrade_0.1.1_amd64.AppImage)

    curl -LO https://github.com/NeoSoul-AI/neotrade-release/releases/download/desktop-v0.1.1/NeoTrade_0.1.1_amd64.AppImage
    chmod +x NeoTrade_0.1.1_amd64.AppImage
    ./NeoTrade_0.1.1_amd64.AppImage

## Installing

### macOS

Open the dmg, drag **NeoTrade** into Applications, then run this once:

    xattr -dr com.apple.quarantine /Applications/NeoTrade.app

Without it macOS refuses the app outright — a downloaded ad-hoc-signed bundle
is blocked at exec on macOS 15 and later. There is no way to do this from the
UI: right-click → Open does not bypass it, and System Settings → Privacy &
Security offers "Open Anyway" only for Developer-ID-signed apps, so the button
never appears.

### Windows

Run setup.exe. SmartScreen warns about an "unknown publisher" because the
installer carries no Authenticode signature: **More info** → **Run anyway**.

### Verifying a download

Every asset ships a matching `.sig`, and each release carries one `SHA256SUMS`
covering all of them:

    curl -LO https://github.com/NeoSoul-AI/neotrade-release/releases/download/desktop-v0.1.1/SHA256SUMS
    shasum -a 256 -c SHA256SUMS --ignore-missing   # sha256sum on Linux

## Updates

Nothing to download by hand after the first install — the app offers every
later release on its channel in place.

Updates are driven by `latest.json`, which installed apps poll. A release is
only reached once a **channel** points at it:

- **stable** (`desktop-channel-stable`) — everyone, by default.
- **beta** (`desktop-channel-beta`) — internal test installs only.

Beta releases are tagged `-beta.N` and marked pre-release. They are internal
test builds; unless you were asked to run one, take the stable release above.

The `.app.tar.gz` assets are the updater's own bundle format. A manual install
never needs them.

## Releases

See [Releases](../../releases). Each release's notes carry its own download
links and install steps, generated from the artifacts that build actually
produced.
