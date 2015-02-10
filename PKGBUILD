# Maintainer: Jashandeep Sohi <jashandeep.s.sohi@gmail.com>

_snapshot="20150208"
_islver=0.14
_gccsrc="gcc-5-$_snapshot"

pkgname='libgccjit'
pkgver="5_$_snapshot"
pkgrel=1
pkgdesc='Just-In-Time Compilation using GCC.'
url='https://gcc.gnu.org/wiki/JIT'
license=('GPL3')
source=(
 "ftp://gcc.gnu.org/pub/gcc/snapshots/5-$_snapshot/$_gccsrc.tar.bz2"
 "ftp://gcc.gnu.org/pub/gcc/infrastructure/isl-$_islver.tar.bz2"
)
md5sums=(
 '0047b8750a606e6f3e57f01b45eba268'
 'acd347243fca5609e3df37dba47fd0bb'
)
arch=('i686' 'x86_64')
depends=(
 'glibc'
)
makedepends=(
 'git'
 'binutils'
 'gcc-ada'
 'libmpc'
)

prepare() {
 cd "$srcdir/$_gccsrc"
 
 ln -sf ../isl-$_islver isl
 
 CPPFLAGS="$CPPFLAGS -O2"
 
}

build() {
 install -d "$srcdir/$pkgname-build"
 cd "$srcdir/$pkgname-build"
 
 ../$_gccsrc/configure \
  --prefix="$pkgdir/usr" \
  --disable-multilib \
  --with-system-zlib \
  --enable-host-shared \
  --enable-languages=jit \
  --disable-bootstrap \
  --enable-checking=release \
  extra_isl_gmp_configure_flags='--enable-shared'
 make
}

check() {
 cd "$srcdir/$pkgname-build"
 make check-jit RUNTESTFLAGS="-v -v -v"
}

package() {
 cd "$srcdir/$pkgname-build"
 make install
}

# vim: tabstop=1
