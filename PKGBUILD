pkgname=brutalchess
pkgver=0.5.2
pkgrel=1
pkgdesc='Chess game with 3D graphics powered by OpenGL and SDL.'
arch=('x86_64')
url='https://sourceforge.net/projects/brutalchess/'
license=('GPL2')
source=("http://ufpr.dl.sourceforge.net/project/brutalchess/brutalchess-alpha/brutalchess-alpha-${pkgver}/brutalchess-alpha-${pkgver}-src.tar.gz" "${pkgname}.desktop" "${pkgname}.png")
depends=("sdl_image" "glu" "freetype2")
md5sums=('370476b63091b8d82a9ea57c604dcbab'
         '98c8d0a7a6d73102db48fda7410aebc4'
         '7fc3c371900324bd742e9ab792ce8dd0')


prepare() {
  cd $pkgname-$pkgver/src
  sed '/<time.h>/ a\#include <limits.h>' -i brutalplayer.cpp
  sed 's/GLvoid/void/g'                  -i {md3view,objview}.cpp
  sed '/<string>/ a\#include <unistd.h>' -i {xboardplayer,faileplayer}.cpp
  sed 's~#include\ <freetype/~#include\ <freetype2/freetype/~g' -i fontloader.h
}

build() {
  cd $pkgname-$pkgver
  ./configure --prefix=/usr --libexecdir=/usr/bin
  make
}

check() {
  cd $pkgname-$pkgver
  make check
}

package() {
    install -Dm644 $srcdir/$pkgname.desktop $pkgdir/usr/share/applications/$pkgname.desktop
    install -Dm644 $srcdir/$pkgname.png $pkgdir/usr/share/pixmaps/$pkgname.png
    cd $pkgname-$pkgver
    make DESTDIR=$pkgdir install
}
