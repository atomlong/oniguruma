# Maintainer: Atom Long <atom.long@hotmail.com>

_realname=onig
pkgname="oniguruma"
pkgver=6.9.8
pkgrel=1
pkgdesc="A regular expressions library (msys2)"
arch=(any)
license=('BSD')
url="https://github.com/kkos/oniguruma"
options=('staticlibs')
makedepends=("autotools" "gcc")
source=("https://github.com/kkos/${pkgname}/releases/download/v${pkgver}/${_realname}-${pkgver}.tar.gz"
        0001-onig-config-win-paths.patch)
sha256sums=('28cd62c1464623c7910565fb1ccaaa0104b2fe8b12bcd646e81f73b47535213e'
            '0163df619698fc1a25733db63538a2e65bdfdc5b19383f1d8bca50d5bbfff0f1')

prepare() {
  cd "${srcdir}/${_realname}-${pkgver%.1}"
  patch -p1 -i "${srcdir}/0001-onig-config-win-paths.patch"

  autoreconf -fiv
}

build() {
  cd "${srcdir}/${_realname}-${pkgver%.1}"
  ../${_realname}-${pkgver%.1}/configure \
      --enable-shared \
      --enable-static \
      --enable-posix-api

  make
}

check() {
  cd "${srcdir}/${_realname}-${pkgver%.1}"
  make check || true
}

package() {
  cd "${srcdir}/${_realname}-${pkgver%.1}"
  make install DESTDIR="${pkgdir}"

  rm -fv "${pkgdir}/usr/lib/libonig.def"

  install -vDm644 "${srcdir}/${_realname}-${pkgver%.1}/COPYING" "${pkgdir}/usr/share/licenses/${_realname}/COPYING"
}
