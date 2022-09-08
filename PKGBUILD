# Maintainer: jmcb <joelsgp@protonmail.com>
# Contributor: webmeister <aur -dot- 20 -dot- webmeister -at- spamgourmet -dot- com>
# Contributor: Christopher Arndt <aur -at- chrisarndt -dot- de>

pkgname=mu-editor
pkgver=1.1.1
pkgrel=1
pkgdesc='A simple Python editor for beginner programmers'
arch=('any')
url='https://codewith.mu/'
license=('GPL3')
# https://github.com/mu-editor/mu/blob/master/setup.py
depends=('python-pyqt5' 'qt5-serialport' 'python-qscintilla-qt5' 'python-pyqt5-chart'
         'python-jupyter_client' 'python-ipykernel' 'python-ipython-genutils'
         'python-qtconsole' 'python-adafruit-board-toolkit' 'python-pyserial' 'python-nudatus'
         'flake8' 'python-click' 'python-black' 'python-platformdirs'
         'python-semver' 'python-virtualenv' 'python-wheel' 'python-requests')
makedepends=('python-setuptools')
checkdepends=('python-pytest' 'python-pytest-cov' 'python-pytest-random-order'
              'python-pytest-timeout' 'python-coverage')
optdepends=('scrapy'
            'python-beautifulsoup4')
source=("https://github.com/mu-editor/mu/archive/refs/tags/v$pkgver.tar.gz"
        "$pkgname.desktop"
        "$pkgname-$pkgver.patch"
        "pyflakes-regex.patch::https://github.com/mu-editor/mu/commit/bc9a13bad85d07300bd6e4f2134d50f49404331d.patch")
sha256sums=('6ea06d09ba0ed15a2bdd87b62ad1c18a0b1edc7000956209720fcc4ad290458e'
            '4a47b1f100a2a77018bae2422cee7bfe2cbea4c9412de1abf646c2fa7a63b62e'
            'e84a04071b9984711df20da5cd1a78a09201c71d4807769fcae57633086545a6'
            'e6895f14c41265423c7a0d5f40ccd4b504d32962bc76cfbf14942429d0bcdf82')

_name=mu


prepare() {
    cd "$_name-$pkgver"
    # Unpin all dependencies, so package doesn't break when a dependency is updated
    patch -p1 -i "$srcdir/$pkgname-$pkgver.patch"
    # Upstream fix for some tests
    patch -p1 -i "$srcdir/pyflakes-regex.patch"
}

build() {
    cd "$_name-$pkgver"
    python setup.py build
}

check() {
    cd "$_name-$pkgver"
    make -k check
}

package() {
    # Desktop entry
    install -Dm644 $pkgname.desktop -t "$pkgdir/usr/share/applications"

    cd "$_name-$pkgver"
    # Desktop icon
    install -Dm644 conf/mu.codewith.editor.png "$pkgdir/usr/share/pixmaps/$pkgname.png"
    # Setuptools install
    python setup.py install --root="$pkgdir/" --optimize=1
}
