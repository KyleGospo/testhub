# Bluefin's OCI Flatpak Remote

An experimental Flatpak remote designed to prototype Flathub's transition to OCI. Someone promised me a magical land of shared storage and composefs, I guess we'll find out. 😄

- Flatpak packaging pipeline with full automation
- Serves the remote from GitHub Pages; pushes images to `ghcr.io/<org>/<repo-name>`
- [Chunkah](https://github.com/coreos/chunkah) and [zstd:chunked](https://github.com/containers/storage/blob/main/docs/containers-storage-zstd-chunked.md) enabled for partial pulls on the client
- Under no circumstance will this remote ever go to production
  - Things the core team wants to test (Ghostty, Goose) to hopefully aid in getting their flatpaks getting submitted to flathub.
  - Purpose is to gather data for using OCI for Flathub distribution.

This potentially unlocks all container registries and git forges as Flatpak hosts in a format supported by flatpak. This is a prototype and not a replacement or substitute for Flathub's official process.

## Key Dependencies

- [Flatpak](https://flatpak.org/) — Application sandboxing and distribution framework
- [OCI Image Format Specification](https://github.com/opencontainers/image-spec) — Standard for container image formats
- [bootc](https://containers.github.io/bootc/) — Transactional, in-place operating system updates using OCI images
- [Podman](https://podman.io/) — Daemonless OCI container engine
- [Skopeo](https://github.com/containers/skopeo) — Tool for inspecting and copying container images
- [flatpak-builder](https://docs.flatpak.org/en/latest/flatpak-builder.html) — Builds Flatpak applications from manifests

## Usage

### Add this remote

Replace `<org>` with the GitHub organization or user and `<repo-name>` with this repository's name:

    flatpak remote-add --if-not-exists testhub oci+https://projectbluefin.github.io/testhub

### Install packages

| Package | App ID | Description |
|---|---|---|
| Ghostty | `com.mitchellh.ghostty` | GPU-accelerated terminal emulator |
| Goose | `io.github.block.Goose` | Goose AI agent |
| Firefox Nightly | `org.mozilla.firefox//nightly` | Firefox Nightly browser |

    flatpak install <repo-name> com.mitchellh.ghostty
    flatpak install <repo-name> io.github.block.Goose
    flatpak install <repo-name> org.mozilla.firefox//nightly

### Update all

    flatpak update

### Checking the Signature

< add instructions here >

### Checking the SBOMs

< add instructions here > 
