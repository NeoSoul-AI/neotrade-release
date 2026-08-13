# neotrade-release

Download artifacts for [NeoTrade](https://neotrade.pro/) — a self-custodial
trading agent runtime. The platform never holds your keys or your funds;
everything security-relevant runs on your own machine.

This repository holds published artifacts only. Source lives elsewhere.

> **Not notarized by Apple, not Authenticode-signed on Windows.** Every bundle
> carries an ed25519 signature verified in CI, but that is artifact integrity,
> not OS trust — so both systems warn on a first install. The two steps that
> get past them are under [Installing](#installing).

## Download

### → [Latest release](../../releases/latest)

That link is permanent and always resolves to the current stable version. This
page deliberately names no version anywhere, so there is nothing here to go
stale between releases.

Open it and pick the file for your platform. The bundles carry the version in
their filename, so what is listed below is the SUFFIX to look for rather than a
link — a per-file URL would have to be rewritten on every release, which is
exactly how the previous version of this page ended up advertising an older
build.

**1. macOS (Apple silicon — M1/M2/M3/M4)** — ends `_aarch64.dmg`

**2. macOS (Intel)** — ends `_x64.dmg`

**3. Windows (x64, installer — recommended)** — ends `_x64-setup.exe`

**4. Windows (x64, msi)** — ends `_x64_en-US.msi`

**5. Linux (Debian/Ubuntu)** — ends `_amd64.deb`

**6. Linux (Fedora/RHEL)** — ends `.x86_64.rpm`

**7. Linux (any distro, AppImage — no install)** — ends `_amd64.AppImage`

The `.sig` files next to them are signatures, and the `.app.tar.gz` pair is the
updater's own bundle format. A manual install needs neither.

### From the command line

One recipe rather than seven URLs, for the same reason: it resolves the newest
release itself, so it keeps working after every release. Set `SUFFIX` from the
list above.

```bash
SUFFIX=_aarch64.dmg
curl -fsSL https://api.github.com/repos/NeoSoul-AI/neotrade-release/releases/latest \
  | grep -o "https://[^\"]*$SUFFIX\"" | tr -d '"' | head -1 | xargs curl -fLO
```

PowerShell — note `curl.exe`, because PowerShell aliases bare `curl` to
`Invoke-WebRequest`, which does not take `-LO`:

```powershell
$suffix = '_x64-setup.exe'
$url = (Invoke-RestMethod https://api.github.com/repos/NeoSoul-AI/neotrade-release/releases/latest).assets |
  Where-Object { $_.name -like "*$suffix" } | Select-Object -First 1 -ExpandProperty browser_download_url
curl.exe -LO $url
```

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

### Linux

From the directory you downloaded into — the globs avoid naming a version:

    sudo apt install ./NeoTrade_*_amd64.deb      # Debian/Ubuntu
    sudo dnf install ./NeoTrade-*.x86_64.rpm     # Fedora/RHEL

The AppImage installs nothing — mark it executable and run it:

    chmod +x NeoTrade_*_amd64.AppImage
    ./NeoTrade_*_amd64.AppImage

### Verifying a download

Every asset ships a matching `.sig`, and each release carries one `SHA256SUMS`
covering all of them. `SHA256SUMS` is one of the few assets whose own name has
no version in it, so this link is permanent too:

    curl -LO https://github.com/NeoSoul-AI/neotrade-release/releases/latest/download/SHA256SUMS
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

## Releases

See [Releases](../../releases). Each release's notes carry its own download
links and install steps, generated from the artifacts that build actually
produced — those links do name a version, on purpose: they address that one
specific release.
