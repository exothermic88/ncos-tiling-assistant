# ncos-tiling-assistant

Packaging for [Tiling Assistant](https://github.com/maugustoldo/cosmic-tiling-manager)
(`tiling-assistant`) — a libcosmic GUI for managing COSMIC window auto-tiling
exceptions (apps that should open floating) — as the `ncos-tiling-assistant`
pacman package for the [ncos repo](https://github.com/exothermic88/ncos-repo).

This repo holds only the PKGBUILD. It does **not** build from source: it
downloads the upstream release AppImage (`v$pkgver`), extracts it, and ships
the contained binary at `/usr/bin/tiling-assistant` plus a desktop entry and
icon. The AppImage runtime is discarded, so there is no FUSE dependency.

## Build

```sh
makepkg -srf
```

## Update to a new upstream release

1. Bump `pkgver` in the PKGBUILD (and reset `pkgrel=1`).
2. `updpkgsums`
3. `makepkg -srf`

Check that the release asset is still named `tiling-assistant-<ver>-x86_64.AppImage`
(upstream renamed it between 1.1.0 and 1.1.1).

## Publish to the ncos repo

```sh
cp ncos-tiling-assistant-<ver>-<rel>-x86_64.pkg.tar.zst ~/claude_projects/ncos-repo/x86_64/
cd ~/claude_projects/ncos-repo
./rename   # repo-add + db rename
git add . && git commit -m "Add ncos-tiling-assistant <ver>-<rel>"
./push
```
