#Maintainer Erik Inkinen <erik.inkinen@gmail.com>
pkgname=halium-wrappers
provides=('halium-wrappers')
_pkgbase=halium-wrappers
pkgver=13.55bd88f
pkgrel=1
arch=('armv7h' 'aarch64' 'x86' 'x86_64')
url="https://github.com/droidian/halium-wrappers"
license=('BSD')
depends=()
makedepends=('git' 'libhybris')
source=("halium-wrappers::git+https://github.com/droidian/halium-wrappers.git")
md5sums=('SKIP')
options=(debug !strip)

pkgver() {
  cd "${srcdir}/${_pkgbase}"
  echo $(git rev-list --count HEAD).$(git rev-parse --short HEAD)
}

build() {
  cd "${srcdir}/${_pkgbase}"
  make build
}

package() {
  cd "${srcdir}/${_pkgbase}/src"
  SYMLINKS=(android_bootctl android_logcat android_lshal android_getprop android_setprop android_reboot logcat lshal)
  install -d ${pkgdir}/usr/bin
  install -d ${pkgdir}/usr/lib/halium-wrappers
  install -d ${pkgdir}/usr/lib/$(gcc -dumpmachine)
  install -m 755 waitforservice ${pkgdir}/usr/bin
  install -m 4644 libtls-padding.so ${pkgdir}/usr/lib/$(gcc -dumpmachine)
  install -m 755 halium-lxc-exec.sh ${pkgdir}/usr/lib/halium-wrappers
  for link in ${SYMLINKS}; do \
    ln -s /usr/lib/halium-wrappers/halium-lxc-exec.sh ${pkgdir}/usr/bin/$${link}; \
  done
}
