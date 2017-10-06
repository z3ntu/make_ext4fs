# $Id$
# Maintainer: Anatol Pomozov
# Contributor: 謝致邦 <Yeking@Red54.com>
# Contributor: Alucryd <alucryd at gmail dot com>

pkgname=android-tools-fsutils
pkgver=8.0.0_r11
pkgrel=1
pkgdesc='Android platform tools-fsutils'
arch=(i686 x86_64)
url='http://tools.android.com/'
license=(Apache MIT)
depends=(pcre2)
optdepends=('python: for mkbootimg script')
makedepends=(git clang gtest ruby cmake ninja go)
source=(git+https://android.googlesource.com/platform/system/core#tag=android-$pkgver
        git+https://android.googlesource.com/platform/system/extras#tag=android-$pkgver
        git+https://android.googlesource.com/platform/external/selinux#tag=android-$pkgver
        generate_build.rb
        fix_build_core.patch
        fix_build_selinux.patch
        canned_revert.patch) # partial revert of system/extras commit aad1accb587aa708012b329c784332dcc9991de6
sha1sums=('SKIP'
          'SKIP'
          'SKIP'
          '795a18c989b6f14c992fa6115903a622646bc157'
          '45e41bab3633bb0be96b238aae3164a5c90721f1'
          'ec473160d7445f97bccabd1c32ac0ae2f77900c1'
          '4588694d06e5ff2e0477646235e3453c26423af3')

prepare() {
  PKGVER=$pkgver ./generate_build.rb > build.ninja

  cd $srcdir/core
  patch -p1 < ../fix_build_core.patch
  
  cd $srcdir/extras
  patch -p1 < ../canned_revert.patch

  cd $srcdir/selinux
  patch -p1 < ../fix_build_selinux.patch
}

build() {
  ninja
}

package(){
  install -m755 -d "$pkgdir"/usr/bin
  install -m755 -t "$pkgdir"/usr/bin make_ext4fs
}
