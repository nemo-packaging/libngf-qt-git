## $Id$
# Contributor: TheKit <nekit1000 at gmail.com>
# Contributor: Alexey Andreyev <aa13q@ya.ru>
# Maintainer: James Kittsmiller (AJSlye) <james@nulogicsystems.com>

pkgname=qt5-ngfd-git
_pkgname=libngf-qt-git
pkgver=0.6.4.r0.g1f3ec8d
pkgrel=1
pkgdesc="Qt-based client library for Non-Graphic Feedback daemon"
arch=('x86_64' 'aarch64')
url="https://git.sailfishos.org/mer-core/libngf-qt"
license=('GPL')
depends=('qt5-declarative' 'libngf')
makedepends=('git')
provides=("${_pkgname%-git}" "${pkgname%-git}")
conflicts=("${_pkgname%-git}" "${pkgname%-git}")
source=('git+https://git.sailfishos.org/mer-core/libngf-qt.git')
md5sums=('SKIP')

pkgver() {
    cd "$srcdir/${_pkgname%-git}"
    git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
    cd "$srcdir/${_pkgname%-git}"
    qmake PREFIX=/usr
	
    # Hack for PREFIX path not being passed to src subproject for some reason
    cd src
    qmake PREFIX=/usr
    cd ..

    make
}

package() {
    cd "$srcdir/${_pkgname%-git}"
    make INSTALL_ROOT="$pkgdir/" install
    # Remove tests
    rm -rf "$pkgdir/opt"
}
