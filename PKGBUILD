# Maintainer: Konstantin Gizdov < arch at kge dot pw >

pkgname=cvmfs
pkgver=2.3.5
pkgrel=3
pkgdesc='A scalable, reliable and low-maintenance software distribution service.'
arch=('i686' 'x86_64')
url='https://cernvm.cern.ch'
license=('BSD')
makedepends=('cmake' 'gtest' 'python-geoip' 'sparsehash')
depends=('curl'
         'c-ares'
         'fuse2'
         'intel-tbb'
         'leveldb'
         'openssl-1.0'
         'pacparser'
         'python'
         'sqlite')
optdepends=()
options=('!emptydirs')
source=("https://github.com/${pkgname}/${pkgname}/archive/${pkgname}-${pkgver}.zip"
        'libexec.patch'
        'settings.cmake')
sha256sums=('ef4bd4ea86832db950cd5b4761fe5c74622ff2f234e57f4cd932ef10aeb1a549'
            '7a33466e3b1763cead058b32fecea35a4a008fdba400e2406243a98305984bfe'
            '559f8ef1a76378cf979b8d507696f97b0a478268f437f773f463a978f994a81e')

prepare() {
    cd "${srcdir}/${pkgname}-${pkgname}-${pkgver}"
    msg2 'Fixing libexec to lib...'
    patch -p1 -i "${srcdir}/libexec.patch"
    msg2 'Fixing /sbin to /usr/bin'
    sed -e "s/\/sbin/\/usr\/bin/g" -i CMakeLists.txt mount/CMakeLists.txt
}

build() {
    cd "${srcdir}"
    mkdir -p build
    cd "${srcdir}/build"
    cmake -C "${srcdir}/settings.cmake" "${srcdir}/${pkgname}-${pkgname}-${pkgver}"

    make ${MAKEFLAGS}
}

package() {
    cd "${srcdir}/build"

    make DESTDIR="${pkgdir}" install
    install -D "${srcdir}/${pkgname}-${pkgname}-${pkgver}/COPYING" "${pkgdir}/usr/share/licenses/cvmfs/COPYING"
}
