# Maintainer: Nicolas Hureau <archlinux@kalenz.fr>

pkgname=ocaml-svn
_pkgname=ocaml
pkgver=13905
pkgrel=1
pkgdesc="A functional language with OO extensions - SVN trunk"
arch=('i686' 'x86_64')
url="http://caml.inria.fr/"
license=('LGPL2' 'custom: QPL-1.0')
depends=('gdbm')
makedepends=('tk' 'ncurses>=5.6-7' 'libx11' 'gcc' 'subversion')
optdepends=('ncurses: advanced ncurses features' 'tk: advanced tk features')
provides=('ocaml')
conflicts=('ocaml')
source=('ocaml::svn+http://caml.inria.fr/svn/ocaml/trunk')
sha256sums=('SKIP')

pkgver() {
  cd "$srcdir/$_pkgname"
  svnversion
}

build() {
  cd "$srcdir/$_pkgname"
  ./configure -prefix /usr
  # Force -j1 or it won't build
  make -j1 world.opt || return 1
}

package() {
  cd "$srcdir/$_pkgname"

  install -D -m 644 LICENSE $pkgdir/usr/share/licenses/ocaml/LICENSE
  make PREFIX=$pkgdir/usr MANDIR=$pkgdir/usr/share/man install || return 1

  # Save >10MB with this one, makepkg only strips debug symbols.
  find $pkgdir/usr/lib -type f -name '*.so.*' -exec strip --strip-unneeded {} \;
}
