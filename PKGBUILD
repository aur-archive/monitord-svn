# Maintainer: Thomas Gatzweiler <thomas.gatzweiler at gmail com>
pkgname=monitord-svn
pkgver=454
pkgrel=2
pkgdesc="Radio signal analyzer for ZVEI, POCSAG and FMS."
arch=(i386 x86_64)
url="http://www.monitord.de"
license=('GPL3')
depends=(lua)
makedepends=(svn)

_svntrunk="http://svn.monitord.de/monitor/trunk/"
_svnmod="monitord"

build() {
  if [ -d ${_svnmod}/.svn ]; then
    (cd "${_svnmod}" && svn cleanup && svn update -r ${pkgver})
  else
    svn co ${_svntrunk} ${_svnmod} -r ${pkgver} --config-dir ./
  fi

  rm -rf build
  cp -rf ${_svnmod} build
  cd build

  chmod +x ./configure
  ./configure --prefix=/usr --enable-plugins --with-mysql
  make
}

package() {
  cd build
  make DESTDIR="${pkgdir}" install
  mkdir -p ${pkgdir}/usr/share/monitord/
  cp sample-config/* ${pkgdir}/usr/share/monitord/
}
