pkgname=(
    libsigc++
    libsigc++-docs
)
pkgbase=libsigc++
pkgver=2.12.1
pkgrel=2
pkgdesc="Callback Framework for C++"
arch=('x86_64')
url="https://libsigcplusplus.github.io/libsigcplusplus/"
license=('LGPL-2.1-or-later')
depends=('gcc-libs')
makedepends=(
    'docbook5-xml'
    'doxygen'
    'graphviz'
    'git'
    'meson'
    'mm-common'
)
source=(git+ssh://git@github.com/libsigcplusplus/libsigcplusplus#commit=6bef4e0005f00f0844d917866aec7e3b2d829fdf)
sha256sums=(d2f6a86863f53f05154ee41b7757d4986e209c05977be0467864487a197cdfe3)

pkgver() {
    cd libsigcplusplus

    git describe --tags | sed 's/[^-]*-g/r&/;s/-/+/g'
}

build() {
    cd libsigcplusplus

    local meson_args=(
        -D maintainer-mode=true
    )

    ${meson_options} "${meson_args[@]}"

    ${meson_build}
}

package_libsigc++ () {
    cd libsigcplusplus

    ${meson_install} ${pkgdir}

    # Split -docs
    _pick docs ${pkgdir}/usr/share/{devhelp,doc}
}

package_libsigc++-docs() {
    pkgdesc+=" (documentation)"
    depends=()
    options=(!strip)

    mv docs/* ${pkgdir}
}
