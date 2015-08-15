# Maintainer: graysky <graysky AT archlinux DOT us>
pkgname=flac2all-svn
_pkgname=flac2all
pkgver=32
pkgrel=1
pkgdesc="Multi-threaded audio converter of FLAC to either Ogg Vorbis or MP3 retaining all tags and metadata. Dev version."
arch=('any')
url="http://code.google.com/p/flac2all"
license=('GPL2')
depends=('flac' 'lame' 'vorbis-tools' 'python2')
makedepends=('subversion')
conflicts=('flac2all')
provides=('flac2all')

_svntrunk=http://flac2all.googlecode.com/svn/trunk/dev
_svnmod=$pkgname-read-only

build() {
  msg "Connecting to SVN server...."

  if [[ -d "$_svnmod/.svn" ]]; then
    (cd "$_svnmod" && svn up -r "$pkgver")
  else
    svn co "$_svntrunk/" --config-dir ./ -r "$pkgver" "$_svnmod"
  fi
  msg "SVN checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_svnmod-build"
  cp -r "$srcdir/$_svnmod" "$srcdir/$_svnmod-build"
}

package() {
  cd "$_svnmod-build"
  
  # set python --> python2 and reset defaults to what are considered transparent for vorbis and lame
  sed -i -e s'/python/python2/1' -i -e s'/quality=2/quality=5/g' -i -e s'/ -q 0//g' flac2all-dev.py
  install -Dm755 flac2all-dev.py "$pkgdir/usr/bin/flac2all"
}

# vim:set ts=2 sw=2 et:
