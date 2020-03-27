# Package maintainer: airwoodix <airwoodix at posteo dot me>

pkgname=hdf5-blosc-filter-git
pkgver=r34.gbd8ee59
pkgrel=1
pkgdesc="Blosc filter for the HDF5 data format"
arch=('i686' 'x86_64')
url="https://github.com/Blosc/hdf5-blosc"
license=('custom')
depends=('hdf5' 'blosc')
makedepends=('git' 'cmake')
source=("${pkgname%-git}::git+https://github.com/Blosc/hdf5-blosc#tag=v1.0.0"
        'no-libblosc.patch')
md5sums=('SKIP'
         '80650fc5a191fc03765babd60ebf294d')
sha256sums=('SKIP'
            'cea4757d245db949e05c21895137ae02146dc34428ea47a5e1ac480b4ff8a21d')

pkgver() {
    cd "${pkgname%-git}"
    printf "r%s.g%s" "$(git rev-list --count HEAD)" \
	   "$(git rev-parse --short HEAD)"
}

prepare() {
    cd "${srcdir}/${pkgname%-git}"
    git apply "${srcdir}/no-libblosc.patch"
}

build() {
    cd "${srcdir}/${pkgname%-git}"
    mkdir -p build && cd build
    cmake .. -DCMAKE_INSTALL_PREFIX=/usr
    make
}

package() {
    cd "${srcdir}/${pkgname%-git}/build"
    make DESTDIR="${pkgdir}/" install
    install -Dm644 "../LICENSES/BLOSC_HDF5.txt" \
	    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
