# Maintainer: Anton Bazhenov <anton.bazhenov at gmail>
# Contributor: Christoph Zeiler <archNOSPAM_at_moonblade.dot.org>

pkgname=primrose
pkgver=6
pkgrel=2
pkgdesc="A captivating tile-clearing puzzle game by Jason Rohrer"
arch=('i686' 'x86_64')
url="http://primrose.sourceforge.net/"
license=('custom:public_domain')
depends=('mesa' 'sdl')
install="${pkgname}.install"
source=("http://downloads.sourceforge.net/${pkgname}/Primrose_v${pkgver}_UnixSource.tar.gz"
        "${pkgname}.png"
        "${pkgname}.desktop"
        "${pkgname}.sh")
md5sums=('3bef20e73e060482ef6602b890751abb'
         '84fcb146c07e443adf881ace6618a9e2'
         'a7e42cfbcfa14d7e3f620050d47ca8e5'
         '571bd25aa9ad988052593dea4e674bdf')

build() {
  cd "${srcdir}/Primrose_v${pkgver}_UnixSource"

  sed -i "s_^./configure_echo 1 | ./configure_" runToBuild
  ./runToBuild
}

package() {
  cd "${srcdir}/Primrose_v${pkgver}_UnixSource"

  # Install game files
  mkdir -p "${pkgdir}/opt/${pkgname}"
  cp -R graphics settings Primrose *.txt "${pkgdir}/opt/${pkgname}"

  # Set permissions
  chgrp -R games "${pkgdir}/opt/${pkgname}"
  chmod -R g+w "${pkgdir}/opt/${pkgname}"

  # Install launchers
  install -Dm755 "../${pkgname}.sh" "${pkgdir}/usr/bin/${pkgname}"
  ln -s "/usr/bin/${pkgname}" "${pkgdir}/usr/bin/Primrose"

  # Install pixmap and .desktop file
  install -Dm644 "../${pkgname}.png" "${pkgdir}/usr/share/pixmaps/${pkgname}.png"
  install -Dm644 "../${pkgname}.desktop" "${pkgdir}/usr/share/applications/${pkgname}.desktop"
}

# vim:set ts=2 sw=2 et:
