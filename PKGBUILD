# Maintainer: webmeister <aur -dot- 20 -dot- webmeister -at- spamgourmet -dot- com>
# Maintainer: Christopher Arndt <aur -at- chrisarndt -dot- de>

pkgname=mu-editor
epoch=1
pkgver=1.0.3
pkgrel=4
pkgdesc='A simple Python editor for beginner programmers'
arch=('any')
url='https://codewith.mu/'
license=('GPL3')
depends=('pigpio' 'python-appdirs' 'python-gpiozero' 'python-guizero'
         'python-matplotlib' 'python-nudatus' 'python-pgzero'
         'python-pycodestyle' 'python-pyflakes' 'python-pyqt5-chart>=5.15'
         'python-pyserial' 'python-qscintilla-qt5' 'python-qtconsole'
         'python-requests' 'python-semver' 'qt5-serialport')
makedepends=('python-setuptools')
source=("https://github.com/mu-editor/mu/archive/$pkgver.tar.gz")
sha256sums=('d9917794de845231ffea671ceff24824bbe342c9d0da4340b237f7a915c0c358')

_name=mu


prepare() {
  cd "$_name-$pkgver"
  # Unpin all dependencies, so package doesn't break when a dependency is updated
  sed -i -e 's/==/>=/g' setup.py
}

build() {
  cd "$_name-$pkgver"
  python setup.py build
}

package() {
  cd "$_name-$pkgver"

  # Setuptools install
  python setup.py install --root="$pkgdir/" --optimize=1

  # Desktop entry
  install -Dm644 $pkgname.desktop -t "$pkgdir/usr/share/applications"
  install -Dm644 conf/mu.codewith.editor.png "$pkgdir/usr/share/pixmaps/$pkgname.png"
}
