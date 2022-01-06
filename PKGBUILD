pkgname=dwm-mobiacikaka-git
_pkgname=dwm
pkgver=6.2.r1887.5d5c5f1
pkgrel=1
pkgdesc="A dynamic window manager for X"
url="http://github.com/Mobiacikaka/dwm"
arch=('i686' 'x86_64')
license=('MIT')
options=(zipman)
depends=('libx11' 'libxinerama' 'libxft')
makedepends=('git')
install=dwm.install

provides=("${_pkgname}")
conflicts=("${_pkgname}")

source=(dwm.desktop
        'git://github.com/Mobiacikaka/dwm.git'
        config.h)
md5sums=('939f403a71b6e85261d09fc3412269ee'
         'SKIP'
         'SKIP') # so you can customize config.h

pkgver(){
  cd $_pkgname
  printf "%s.r%s.%s" "$(awk '/^VERSION =/ {print $3}' config.mk)" \
    "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
  cd $srcdir/${_pkgname}
  if [[ -f "$srcdir/config.h" ]]; then
    cp -fv "$srcdir/config.h" config.h
  fi
}

build() {
  cd $_pkgname
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
  cd ${_pkgname}
  make PREFIX=/usr DESTDIR="$pkgdir" install
  install -m644 -D LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -m644 -D README "$pkgdir/usr/share/doc/$pkgname/README"
  install -m644 -D ../dwm.desktop "$pkgdir/usr/share/xsessions/dwm.desktop"
}

# vim:set ts=2 sw=2 et:
