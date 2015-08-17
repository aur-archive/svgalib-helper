# Maintainer: Kristoffer Haavik <kh at kristofferhaavik dot no>
# Contributor: kfgz <kfgz at interia pl>
# Contributor: Link Dupont <link at dot subpop dot net>
# Contributor: u8sand <u8sand at gmail dot com>

pkgname=svgalib-helper
pkgver=1.9.25
pkgrel=3
pkgdesc="A low-level SuperVGA graphics library"
arch=('i686' 'x86_64')
url="http://www.svgalib.org/"
license=('GPL')
depends=('perl')
makedepends=('linux-headers')
install=svgalib-helper.install
source=(http://www.svgalib.org/svgalib-${pkgver}.tar.gz
        svgalib-1.9.25-linux2.6.patch
        svgalib-1.9.25-linux2.6.28.patch
        svgalib-1.9.25-linux2.6.36.patch
				svgalib-1.9.25-linux3.4.patch)
md5sums=('4dda7e779e550b7404cfe118f1d74222'
         'eadd4d3974a475ccc9d72f1e614c69df'
         '5c797ca334e4c7f326dc08df7a3eb5c9'
         '99e767dec306ff4d307eef151f352466'
	 			 '01e1c8ccae8dea2776125a4a4f3dc084')

build() {
  cd "${srcdir}"

  patch -Np1 -i "${srcdir}"/svgalib-1.9.25-linux2.6.patch
  patch -Np1 -i "${srcdir}"/svgalib-1.9.25-linux2.6.28.patch
  patch -Np1 -i "${srcdir}"/svgalib-1.9.25-linux2.6.36.patch

  patch -Np1 -i "${srcdir}"/svgalib-1.9.25-linux3.4.patch

  cd svgalib-${pkgver}/kernel/svgalib_helper
  sed -i "s|#include <linux/smp_lock.h>||g" main.c
  
  make
}

package() {
  cd svgalib-${pkgver}/kernel/svgalib_helper
  install -Dm644 svgalib_helper.ko "${pkgdir}"/lib/modules/`uname -r`/misc/svgalib_helper.ko
}
