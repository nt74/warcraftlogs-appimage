# Maintainer: Nikos Toutountzoglou <nikos.toutou@gmail.com>
pkgname=warcraftlogs-appimage
pkgver=6.0.1
pkgrel=1
pkgdesc="Warcraft Logs Uploader, allows you to upload log files for analysis"
arch=('any')
url="https://warcraftlogs.com/"
license=('custom')
depends=('fuse2')
provides=("warcraftlogs-appimage=$pkgver")
conflicts=('warcraftlogs-appimage' 'warcraftlogsuploader')
source=("https://github.com/RPGLogs/Uploaders-warcraftlogs/releases/download/v${pkgver}/Warcraft-Logs-Uploader-${pkgver}.AppImage"
	'warcraftlogs.sh')
sha256sums=('1663ea5f2028df344ed54a69c587bc606ecc1be5258be4d5afdcbc21e180a154'
            '3a961a492b11eb7b8fb897a304964067105b4edea0306d304d493c7c225564de')
options=(!strip) # necessary otherwise the AppImage file in the package is truncated
_image="$(basename "${source[0]}")"

prepare() {
	cd "$srcdir"
	chmod +x "$_image"
	./"$_image" --appimage-extract
	sed -i -e "s/AppRun/\/usr\/bin\/warcraftlogs/" "$srcdir/squashfs-root/warcraftlogs.desktop"
}

package() {
	install -Dm755 "$srcdir/$_image" "$pkgdir/opt/warcraftlogs/warcraftlogs.AppImage"
	install -Dm755 "$srcdir/warcraftlogs.sh" "$pkgdir/usr/bin/warcraftlogs"
	install -dm755 "$pkgdir/usr/share/"
	cp -r --no-preserve=mode,ownership "$srcdir/squashfs-root/usr/share/icons" "$pkgdir/usr/share/"
	install -Dm644 "$srcdir/squashfs-root/warcraftlogs.desktop" "$pkgdir/usr/share/applications/warcraftlogs.desktop"
}