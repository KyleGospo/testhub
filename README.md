# OCI Flatpak Remote

An experimental Flatpak remote designed to prototype Flathub's transition to OCI. Someone promised me a magical land of shared storage and composefs, I guess we'll find out. 😄

- Flatpak packaging pipeline with full automation
- Serves the remote from GitHub Pages; pushes images to `ghcr.io/<org>/<repo-name>`
- [Chunkah](https://github.com/coreos/chunkah) and [zstd:chunked](https://github.com/containers/storage/blob/main/docs/containers-storage-zstd-chunked.md) enabled for partial pulls
- We need data when this lands in OS bootc images so we might as well get going.

This potentially unlocks all container registries and git forges as Flatpak hosts in a format supported by flatpak. This is a prototype and not a replacement or substitute for Flathub's official process, this is designed to test the package format changes.

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

    flatpak remote-add --if-not-exists <repo-name> oci+https://<org>.github.io/<repo-name>

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
