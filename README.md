# neoclaw-release

Download artifacts for [neoclaw](https://neosoul.ai/) — a self-custodial
trading agent runtime for prediction markets.

This repository holds published artifacts only. Source lives elsewhere.

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
builds, not stable versions.
