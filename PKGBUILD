# Maintainer: Christopher Schwaab -- christopher.schwaab gmail
pkgname=qt-gstreamer-git
pkgver=9999
pkgrel=2
pkgdesc="Gstreamer bindings for C++/Qt."
arch=('i686' 'x86_64')
url="http://gitorious.org/qtgstreamer"
license=('GPL')
depends=('gstreamer0.10-base' 'qt4' 'mesa')
makedepends=('cmake' 'flex' 'bison' 'automoc4' 'git' 'boost' 'doxygen')
provides=('qt-gstreamer')
conflicts=('qt-gstreamer' 'qtgstreamer')

_gitroot=git://anongit.freedesktop.org/gstreamer/qt-gstreamer
_gitname=qtgstreamer

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [ -d $_gitname ] ; then
    cd $_gitname && git pull origin
    msg "The local files are updated."
  else
    git clone $_gitroot $_gitname
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting make..."

  rm -rf "$srcdir/$_gitname-build"
  git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"
  cd "$srcdir/$_gitname-build"

  cmake -DCMAKE_INSTALL_PREFIX=/usr -DQT_QMAKE_EXECUTABLE=/usr/bin/qmake-qt4.
  make
}

package() {
  cd "$srcdir/$_gitname-build"
  make DESTDIR="$pkgdir/" install
} 
