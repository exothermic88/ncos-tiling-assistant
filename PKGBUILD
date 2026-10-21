# Maintainer: nic <nicolasciampa2001@gmail.com>
# Personal-repo PKGBUILD: repackages the upstream Tiling Assistant AppImage
# (binary extracted, AppImage runtime discarded). Bump pkgver + updpkgsums to update.
pkgname=ncos-tiling-assistant
_upstream=tiling-assistant
_appid=io.github.maugustoldo.TilingAssistant
pkgver=1.1.1
pkgrel=1
pkgdesc="COSMIC GUI to manage window auto-tiling exceptions (apps that open floating) - Tiling Assistant"
arch=('x86_64')
url="https://github.com/maugustoldo/cosmic-tiling-manager"
license=('MIT')
depends=('libxkbcommon' 'wayland') # wayland: libwayland-client is dlopen'd at runtime
provides=('tiling-assistant')
conflicts=('tiling-assistant')
options=('!debug') # prebuilt binary: no useful debug package to split out
source=("$_upstream-$pkgver-x86_64.AppImage::$url/releases/download/v$pkgver/$_upstream-$pkgver-x86_64.AppImage")
sha256sums=('5263243c8516f0dec0d9c98889d3994b9c0eb177f2edd31b07b16ce6544859ed')

prepare() {
    chmod +x "$_upstream-$pkgver-x86_64.AppImage"
    # --appimage-extract unpacks the embedded squashfs without needing FUSE.
    "./$_upstream-$pkgver-x86_64.AppImage" --appimage-extract >/dev/null
}

package() {
    cd squashfs-root
    install -Dm755 "usr/bin/$_upstream" "$pkgdir/usr/bin/$_upstream"
    install -Dm644 "$_appid.svg" \
        "$pkgdir/usr/share/icons/hicolor/scalable/apps/$_appid.svg"

    # Upstream .desktop has a Portuguese Comment; rewrite in English, keep its WMClass.
    install -d "$pkgdir/usr/share/applications"
    cat > "$pkgdir/usr/share/applications/$_appid.desktop" <<EOF
[Desktop Entry]
Version=1.0
Type=Application
Name=Tiling Assistant
Comment=Manage COSMIC auto-tiling exceptions (apps that should open floating)
Exec=$_upstream
Icon=$_appid
Terminal=false
Categories=Settings;System;DesktopSettings;
StartupWMClass=com.system76.CosmicTilingManager
EOF
}
