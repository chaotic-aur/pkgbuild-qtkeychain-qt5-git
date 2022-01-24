# Maintainer: Antonio Rojas <arojas@archlinux.org>
# Contributor: Kuba Serafinowski <zizzfizzix(at)gmail(dot)com>
# Contributor: Teo Mrnjavac <teo@kde.org>

pkgname=(qtkeychain-qt5-git)
pkgver=_r352.g4dea5e3
pkgrel=1
pkgdesc='Provides support for secure credentials storage'
arch=(x86_64)
url='https://github.com/frankosterfeld/qtkeychain'
license=(BSD)
depends=(libsecret kwallet-git)
makedepends=(cmake-git qt5-tools qt5-base git)
conflicts=(${pkgname%-git})
provides=(${pkgname%-git})
groups=(kdepim-git)
source=("git+https://github.com/frankosterfeld/${pkgname%-qt5-git}.git")
sha256sums=('SKIP')


build() {
  cmake -B build-qt5 -S ${pkgname%-qt5-git} \
    -DCMAKE_INSTALL_PREFIX=/usr
  cmake --build build-qt5
}

package() {
  DESTDIR="$pkgdir" cmake --install build-qt5
  install -Dm644 ${pkgname%-qt5-git}/COPYING "$pkgdir"/usr/share/licenses/${pkgname%-qt5-git}/LICENSE
}

pkgver() {
  cd ${pkgname%-qt5-git}
  _ver="$(grep -m1 'set(RELEASE_SERVICE_VERSION' CMakeLists.txt | cut -d '"' -f2 | tr - .)"
  _ver=${_ver:-"$(grep -m1 'set(PIM_VERSION' CMakeLists.txt | cut -d '"' -f2 | tr - .)"}
  echo "${_ver}_r$(git rev-list --count HEAD).g$(git rev-parse --short HEAD)"
}
