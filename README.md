# neotrade-release

Download artifacts for [NeoTrade](https://neotrade.pro/) — a self-custodial
trading agent runtime. The platform never holds your keys or your funds;
everything security-relevant runs on your own machine.

This repository holds published artifacts only. Source lives elsewhere.

> **macOS bundles are Developer ID signed and Apple-notarized. The Windows
> installer carries no Authenticode signature.** So macOS opens the app
> directly, while SmartScreen still warns on a first Windows install — the one
> click that gets past it is under [Installing](#installing). Every bundle also
> carries an ed25519 signature verified in CI, which is artifact integrity
> rather than OS trust.

**[What's new](CHANGELOG.md)** — every stable release's notes on one page,
newest first.

## Download

Every link below is permanent and always serves the newest stable release.
Bookmark them, paste them into a message, write them into a doc — nothing here
names a version, so nothing here needs editing when one ships.

They are assets of [`desktop-stable-latest`](../../releases/tag/desktop-stable-latest),
one release that CI republishes with the current bundles under these fixed
names every time a stable version goes out.

**1. macOS (Apple silicon — M1/M2/M3/M4)**

Download: https://github.com/NeoSoul-AI/neotrade-release/releases/download/desktop-stable-latest/neotrade-macos-aarch64.dmg

    curl -LO https://github.com/NeoSoul-AI/neotrade-release/releases/download/desktop-stable-latest/neotrade-macos-aarch64.dmg

**2. macOS (Intel)**

Download: https://github.com/NeoSoul-AI/neotrade-release/releases/download/desktop-stable-latest/neotrade-macos-x64.dmg

    curl -LO https://github.com/NeoSoul-AI/neotrade-release/releases/download/desktop-stable-latest/neotrade-macos-x64.dmg

**3. Windows (x64, setup.exe — recommended)**

Download: https://github.com/NeoSoul-AI/neotrade-release/releases/download/desktop-stable-latest/neotrade-windows-x64-setup.exe

In PowerShell, `curl` is an alias for `Invoke-WebRequest`; call `curl.exe`:

    curl.exe -LO https://github.com/NeoSoul-AI/neotrade-release/releases/download/desktop-stable-latest/neotrade-windows-x64-setup.exe

**4. Windows (x64, msi)**

Download: https://github.com/NeoSoul-AI/neotrade-release/releases/download/desktop-stable-latest/neotrade-windows-x64.msi

    curl.exe -LO https://github.com/NeoSoul-AI/neotrade-release/releases/download/desktop-stable-latest/neotrade-windows-x64.msi

**5. Linux (Debian/Ubuntu, .deb)**

Download: https://github.com/NeoSoul-AI/neotrade-release/releases/download/desktop-stable-latest/neotrade-linux-amd64.deb

    curl -LO https://github.com/NeoSoul-AI/neotrade-release/releases/download/desktop-stable-latest/neotrade-linux-amd64.deb
    sudo apt install ./neotrade-linux-amd64.deb

**6. Linux (Fedora/RHEL, .rpm)**

Download: https://github.com/NeoSoul-AI/neotrade-release/releases/download/desktop-stable-latest/neotrade-linux-x86_64.rpm

    curl -LO https://github.com/NeoSoul-AI/neotrade-release/releases/download/desktop-stable-latest/neotrade-linux-x86_64.rpm
    sudo dnf install ./neotrade-linux-x86_64.rpm

**7. Linux (any distro, AppImage — no install)**

Download: https://github.com/NeoSoul-AI/neotrade-release/releases/download/desktop-stable-latest/neotrade-linux-x86_64.AppImage

    curl -LO https://github.com/NeoSoul-AI/neotrade-release/releases/download/desktop-stable-latest/neotrade-linux-x86_64.AppImage
    chmod +x neotrade-linux-x86_64.AppImage
    ./neotrade-linux-x86_64.AppImage

Want a specific version instead of the newest one? The
[latest release](../../releases/latest) page — and every entry under
[Releases](../../releases) — carries the same bundles under filenames that do
name their version, alongside that version's notes.

## Installing

### macOS

Open the dmg and drag **NeoTrade** into Applications. That is the whole
install: the bundle is Developer ID signed and Apple-notarized, so it opens
directly with no Gatekeeper prompt and no terminal step.

Releases before 0.1.10 were ad-hoc signed and did need a `xattr -dr
com.apple.quarantine` on the installed app. They are not being re-signed, so
take a current version rather than an old one.

### Windows

Run setup.exe. SmartScreen warns about an "unknown publisher" because the
installer carries no Authenticode signature: **More info** → **Run anyway**.

### Linux

The `apt` / `dnf` / `chmod` lines are in each download block above.

### Verifying a download

Every bundle ships a matching `.sig`, and the page carries one `SHA256SUMS`
covering all of them. Take it from the same place you took the bundle — its
lines name these fixed filenames, so a `SHA256SUMS` from a versioned release
would match none of them:

    curl -LO https://github.com/NeoSoul-AI/neotrade-release/releases/download/desktop-stable-latest/SHA256SUMS
    shasum -a 256 -c SHA256SUMS --ignore-missing   # sha256sum on Linux

## Updates

Nothing to download by hand after the first install — the app offers every
later release on its channel in place. The links above are for a FIRST install;
the updater never uses them.

Updates are driven by `latest.json`, which installed apps poll. A release is
only reached once a **channel** points at it:

- **stable** (`desktop-channel-stable`) — everyone, by default.
- **beta** (`desktop-channel-beta`) — internal test installs only.

Beta releases are tagged `-beta.N` and marked pre-release. They are internal
test builds with their own app identity (`NeoTrade-Beta`), installable
alongside the stable app; unless you were asked to run one, take the downloads
above. They have their own permanent page,
[`desktop-beta-latest`](../../releases/tag/desktop-beta-latest).

The `.app.tar.gz` assets on the versioned releases are the updater's own bundle
format. A manual install never needs them.

## Releases

See [Releases](../../releases). Each release's notes carry its own download
links and install steps, generated from the artifacts that build actually
produced — those links do name a version, on purpose: they address that one
specific release.

That list is one entry per build, and most entries are internal-test betas. To
read what changed across versions instead, use [CHANGELOG.md](CHANGELOG.md):
every stable release's notes on one page, newest first.
