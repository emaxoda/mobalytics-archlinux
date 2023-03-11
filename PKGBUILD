pkgname=mobalytics-desktop
pkgver=1.103.5
pkgrel=1
pkgdesc="Mobalytics repackaged  for Linux"
arch=('x86_64')
url="https://github.com/emaxoda/mobalytics-repackager"
license=('UNLICENSED')
depends=('c-ares'  'ffmpeg'  'gtk3'  'http-parser'  'libevent'  'libvpx'  'libxslt'  'libxss'  'minizip' 'nss'  're2'  'snappy'  'libnotify'  'libappindicator-gtk3')
makedepends=('npm')
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/emaxoda/mobalytics-repackager/archive/refs/tags/v${pkgver}.zip"
        builder.diff
        mobalytics-desktop.desktop)
md5sums=('8a862a24c7f5eb5b15a15456e6908884'
            'f4624977f2981f40376beb11a637f29b'
            'd8ec3818788bd43234f3d15243f15808')

prepare(){

  cd "$srcdir/mobalytics-repackager-$pkgver"
  patch -Np1 < "$srcdir/builder.diff"
}

build() {
  cd "$srcdir/mobalytics-repackager-$pkgver"
  npm install
}

package() {
  mkdir -p -m 0755 "${pkgdir}/opt/${_pkgname}/"
  mv "$srcdir/mobalytics-repackager-$pkgver/dist/linux-unpacked" "${pkgdir}/opt/${pkgname}"
	install -Dm0644 -t "$pkgdir/usr/share/applications/" "mobalytics-desktop.desktop"
  for size in 24 32 48 64 128 256 512; do
        install -Dm644 "$srcdir/mobalytics-repackager-$pkgver/app/resources/icons/${size}x${size}.png" \
            "${pkgdir}/usr/share/icons/hicolor/${size}x${size}/apps/mobalytics-desktop.png"
    done
}
