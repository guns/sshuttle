# Current Maintainer: Sung Pae <self@sungpae.com>
# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: alphazo <alphazo@gmail.com>

pkgname=sshuttle-nerv
provides=('sshuttle')
conflicts=('sshuttle' 'sshuttle-alt')
replaces=('sshuttle' 'sshuttle-alt')
groups=('nerv')
pkgver=sshuttle.0.61.5.g312f244
pkgrel=1
pkgdesc="Transparent proxy server that works as a poor man's VPN. Personal for of original apenwarr trunk."
arch=('any')
url="https://github.com/guns/sshuttle"
license=('GPL2')
depends=('python2' 'iptables' 'openssh' 'net-tools')
makedepends=('python2-markdown' 'python2-beautifulsoup3' 'git')
source=("arch-install.patch")
md5sums=('15ed72e2b68dd07ef97abfdcb828d188')

pkgver() {
    printf %s "$(git describe --long | tr - .)"
}

prepare() {
  cd "$startdir"
  patch -p1 -i "$srcdir/arch-install.patch"

  sed -i 's#/usr/bin/env python#/usr/bin/env python2#' stresstest.py Documentation/md2man.py
}

build() {
  cd "$startdir"
  make
}

package() {
  cd "$startdir"
  install -Dm755 sshuttle "$pkgdir/usr/bin/sshuttle"

  install -d "$pkgdir/usr/share/sshuttle"
  cp -r *.py compat "$pkgdir/usr/share/sshuttle"/

  install -d "$pkgdir/usr/share/sshuttle/version"
  cp -r version/*.py "$pkgdir/usr/share/sshuttle/version"

  install -Dm644 Documentation/sshuttle.8 "$pkgdir/usr/share/man/man8/sshuttle.8"
}
