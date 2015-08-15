# Maintainer:  hbdee <hbdee.arch@gmail.com>

pkgname=cantata-kde-svn
pkgver=r5675
pkgrel=2
pkgdesc="KDE client for the music player daemon (MPD) - svn version"
arch=('i686' 'x86_64')
url="https://code.google.com/p/cantata/"
license=('GPL')
depends=('kdebase-runtime' 'libmtp' 'libcddb' 'libmusicbrainz5' 'mpg123' 'taglib-extras' 'hicolor-icon-theme' 'cdparanoia' 'speexdsp' 'media-player-info')
optdepends=('perl-uri: dynamic playlist'
            'mpd: playback')
makedepends=('subversion' 'cmake' 'automoc4')
conflicts=('cantata' 'cantata-kde' 'cantata-svn')
provides=('cantata')
source=("$pkgname::svn+http://cantata.googlecode.com/svn/trunk/")
install="$pkgname.install"
md5sums=('SKIP')

pkgver() {
  cd "${pkgname}"
  local ver="$(svnversion)"
  printf "r%s" "${ver//[[:alpha:]]}"
}

prepare() {
  if [[ -d build ]]
  then
    rm -rf build
  fi
   mkdir build
}

build() {
  cd "$srcdir/build"
  
  cmake ../${pkgname} \
    -DCMAKE_INSTALL_PREFIX=`kde4-config --prefix` \
    -DCMAKE_BUILD_TYPE=Release \
    -DENABLE_HTTP_STREAM_PLAYBACK=ON \
    -DENABLE_KDE=ON
    
  make
}

package() {
  cd "$srcdir/build"

  make DESTDIR="$pkgdir" PREFIX=`kde4-config --prefix` install
}
