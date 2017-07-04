pkgname=mgba
pkgver=0.6
_pkgver=b1
pkgrel=1
arch=('x86_64')
url='http://mgba.io'
license=('custom:MPL2')
makedepends=('cmake' 'qt5-multimedia' 'sdl2' 'zlib' 'libpng' 'libzip' 'libedit'
             'ffmpeg' 'imagemagick' 'desktop-file-utils' 'qt5-tools')
source=(https://github.com/mgba-emu/mgba/archive/$pkgver-$_pkgver.tar.gz)
md5sums=('a97564515381b9d1fa622238e6800f16')

prepare() {
  [[ ! -d build ]] && mkdir build || rm -rf build
}

build() {
  #cd $srcdir/build
  cmake "$srcdir"/mgba-$pkgver-$_pkgver -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_INSTALL_LIBDIR=lib
  make
}


package() {
  pkgdesc='A Nintendo Gameboy Advance Emulator focusing on both speed and accuracy. Qt5 UI.'

  cmake -DCOMPONENT=mgba-qt mgba-$pkgver -DCMAKE_INSTALL_PREFIX="$pkgdir/usr" \
    -P build/cmake_install.cmake
  cmake -DCOMPONENT=libmgba mgba-$pkgver -DCMAKE_INSTALL_PREFIX="$pkgdir/usr" \
    -P build/cmake_install.cmake

  desktop-file-install mgba-$pkgver/res/mgba-qt.desktop --dir "$pkgdir"/usr/share/applications/
  install -Dm644 mgba-$pkgver/res/mgba-256.png "$pkgdir"/usr/share/pixmaps/mgba.png
  install -Dm644 mgba-$pkgver/LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
  install -d "$pkgdir"/usr/share/licenses/$pkgname
}
