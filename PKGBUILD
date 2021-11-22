# Maintainer: Hu Butui <hot123tea123@gmail.com>

_realname=mimalloc
pkgbase=mingw-w64-${_realname}
pkgname=("${MINGW_PACKAGE_PREFIX}-${_realname}")
pkgver=2.0.3
pkgrel=1
pkgdesc="A compact general purpose allocator with excellent performance"
arch=('any')
mingw_arch=('mingw32' 'mingw64' 'ucrt64' 'clang64' 'clang32')
url="https://github.com/microsoft/mimalloc"
license=('MIT')
depends=(
  "${MINGW_PACKAGE_PREFIX}-gcc-libs"
)
makedepends=("${MINGW_PACKAGE_PREFIX}-cmake")
source=("${_realname}-${pkgver}.tar.gz::https://github.com/microsoft/mimalloc/archive/refs/tags/v${pkgver}.tar.gz")
sha256sums=('5af497f360879bf9d07a5146961d275a25f4177fbe21ee6c437db604422acd60')
build() {
  MSYS2_ARG_CONV_EXCL="-DCMAKE_INSTALL_PREFIX=" \
  ${MINGW_PREFIX}/bin/cmake.exe \
    -B "${srcdir}/build-${MINGW_CHOST}" \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX=${MINGW_PREFIX} \
    -DMI_BUILD_SHARED=ON \
    -DMI_BUILD_STATIC=ON \
    -DMI_BUILD_TESTS=OFF \
    -S ${_realname}-${pkgver} \
    -G'MSYS Makefiles'
  ${MINGW_PREFIX}/bin/cmake.exe --build "${srcdir}/build-${MINGW_CHOST}"
}

package() {
  DESTDIR="${pkgdir}" \
  ${MINGW_PREFIX}/bin/cmake.exe \
    --build "${srcdir}/build-${MINGW_CHOST}" \
    --target install
}
