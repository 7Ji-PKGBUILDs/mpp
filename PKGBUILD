# Maintainer: 7Ji <pugokushin@gmail.com>
# Contributor: Mahmut Dikcizgi <boogiepop a~t gmx com>

pkgname='mpp'
pkgver='1.0.3'
pkgrel=2
pkgdesc='Rockchip VPU Media Process Platform (MPP) for hardware video decode'
arch=('x86_64' 'aarch64' 'arm7h')
url='https://github.com/rockchip-linux/mpp'
license=('Apache')
depends=('gcc-libs' 'coreutils' 'udev')
makedepends=('cmake')
provides=(rockchip-mpp="${pkgver}")
conflicts=(rockchip-mpp)
options=(!lto strip)
install='install'
source=(
  "git+${url}.git#tag=${pkgver}"
  '60-mpp.rules'
  'install'
)
sha256sums=('SKIP'
  '05c4e6bf492d982db968e4f0a679634688c08c295f975a884cb2a4b12c65ab86'
  'e41004dc18f77d37b23f84464c4367c7ccf94d8e86b6f751437b685322e153d2'
)

build() {
  cmake -S mpp -B build \
    -DCMAKE_BUILD_TYPE=Release
  cmake --build build
}

package() {
  cmake --install build --prefix "${pkgdir}/usr"

  # mpp needs to access /dev/mpp_service /dev/rga /dev/dma_heap/ and so on
  # access to those devices are +rw'ed to video groups with those rules
  install -m644 -Dt "${pkgdir}/usr/lib/udev/rules.d" 60-mpp.rules
}
