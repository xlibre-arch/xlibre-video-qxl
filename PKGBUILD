# Maintainer: artist for Artix Linux and XLibre <artist@artixlinux.org>

pkgname=xlibre-video-qxl
pkgver=25.0.0
pkgrel=6
pkgdesc='XLibre fork of X.Org X11 qxl video driver'
arch=('x86_64')
license=('MIT')
_pkgname="${pkgname//xlibre/xf86}"
url="https://github.com/X11Libre/${_pkgname}"
depends=("xlibre-xserver>=${pkgver%.*}" 'glibc')
makedepends=("xlibre-xserver-devel>=${pkgver%.*}" 'xorgproto')
conflicts=("${_pkgname}")
provides=("${_pkgname}")
source=("${url}/archive/refs/tags/xlibre-${_pkgname}-${pkgver}.tar.gz")
groups=('xlibre-drivers')
depends+=('spice' 'libxfont2')
makedepends+=('libcacard')
optdepends=('python: for Xspice')

build() {
  cd ${_pkgname}-xlibre-${_pkgname}-${pkgver}
  export CFLAGS=${CFLAGS/-fno-plt}
  export CXXFLAGS=${CXXFLAGS/-fno-plt}
  export LDFLAGS=${LDFLAGS/-Wl,-z,now}

  autoreconf -fi
  ./configure --enable-xspice --prefix=/usr
  make
}

package() {
  cd ${_pkgname}-xlibre-${_pkgname}-${pkgver}
  make DESTDIR="${pkgdir}/" install

  install -v -Dm0755 scripts/Xspice "${pkgdir}"/usr/bin/Xspice
  install -Dm644 "${srcdir}"/${_pkgname}-xlibre-${_pkgname}-${pkgver}/COPYING "${pkgdir}"/usr/share/licenses/${pkgname}/LICENSE
}

sha256sums=('ee0b0798a2fa2dd3e2494dee996cdc41ac2e43054f53b33a619960786d5b7e8c')
