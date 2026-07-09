# Maintainer: workonfire <kolucki62@gmail.com>

_pkgname=stackslib
pkgname=python-stackslib
pkgver=1.0.0a1
pkgrel=1
pkgdesc="UNO card game engine and multiplayer server"
arch=('any')
url="https://github.com/workonfire/stackslib"
license=('GPL-3.0-or-later')
depends=('python' 'python-websockets')
makedepends=('python-build' 'python-installer' 'python-wheel' 'python-hatchling')
source=("${_pkgname}-${pkgver}.tar.gz::${url}/archive/refs/tags/v${pkgver}.tar.gz")
sha256sums=('SKIP')

build() {
	cd "$srcdir/${_pkgname}-${pkgver}"
	python -m build --wheel --no-isolation
}

package() {
	cd "$srcdir/${_pkgname}-${pkgver}"
	python -m installer --destdir="$pkgdir" dist/*.whl
	install -Dm644 LICENSE "$pkgdir/usr/share/licenses/${pkgname}/LICENSE"
}
