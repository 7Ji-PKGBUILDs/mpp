# Maintainer: 7Ji <pugokushin@gmail.com>
# Contributor: Mahmut Dikcizgi <boogiepop a~t gmx com>

pkgname='mpp'
pkgver='1.0.3'
pkgrel=1
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
sha256sums=(
  'SKIP'
  '4bc41c840642ed4d20a4e696ba623d3d1764b557ab65a69a328cd372e813c705'
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
