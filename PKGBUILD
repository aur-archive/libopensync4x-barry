# Maintainer: Thibi <thibitian [at] gmail.com>

# libopensync
# Contributor: Sergej Pupykin
# Contributor: Hauke Wesselmann <hauke@h-dawg.de>
# Contributor: Laurie Clark-Michalek <bluepeppers@archlinux.us>

#plugin-evolution3
# Contributor: William Rea <sillywilly@gmail.com>
# Contributor: Giorgio Lando <patroclo7@gmail.com>
# Contributor: Sven Salzwedel <sven_salzwedel@web.de>
# Contributor: Hauke Wesselmann <hauke@h-dawg.de>

#plugin-file
# Contributor: William Rea <sillywilly@gmail.com>
# Contributor: Giorgio Lando <patroclo7@gmail.com>
# Contributor: Sven Salzwedel <sven_salzwedel@web.de>
# Contributor: Hauke Wesselmann <hauke@h-dawg.de>

#plugin-google-calendar
# Contributor: Nicolas Quienot <niQo>

#plugin-vformat
# Contributor: William Rea <sillywilly@gmail.com> , Robert Emil Berge <filoktetes@linuxophic.org>
# Contributor: Hauke Wesselmann <hauke@h-dawg.de>

#plugin-xmlformat
# Contributor: William Rea <sillywilly@gmail.com> , Robert Emil Berge <filoktetes@linuxophic.org>
# Contributor: Hauke Wesselmann <hauke@h-dawg.de>

pkgbase=libopensync4x-barry
pkgname=('libopensync' 'osynctool'
    'libopensync-plugin-evolution3' 'libopensync-plugin-file'
    'libopensync-plugin-google-calendar' 
    'libopensync-plugin-vformat' 'libopensync-plugin-xmlformat')
pkgdesc="Barry snapshot of the OpenSync 0.4x synchronisation framework. It also builds most of the OpenSync plugins for compatibility."
pkgver=0.39
pkgrel=1
_realrel=201205242346
arch=('i686' 'x86_64')
url='http://www.opensync.org'
license=('LGPL' 'GPL')
makedepends=('cmake')
optdepends=('osynctool' 'libopensync-plugin-evolution3'
    'libopensync-plugin-file' 'libopensync-plugin-google-calendar' 
    'libopensync-plugin-vformat' 'libopensync-plugin-xmlformat')
source=("http://downloads.sourceforge.net/barry/binary-meta-snapshot-${_realrel}.tar.bz2")
md5sums=('68f83e1af245772b3ccc48d3c3a82066')

build() {
  mv ${srcdir}/binary-meta-snapshot-${_realrel}/sources/ $srcdir/
}

package_libopensync() {
pkgname=('libopensync')
pkgdesc="Barry snapshot of the OpenSync 0.4x synchronisation framework."
license=('LGPL')
depends=('glib2' 'libxml2' 'sqlite3' 'libxslt')
makedepends=('python2' 'chrpath')
provides=('libopensync=0.39')
conflicts=('libopensync' 'libopensync-stable')
replaces=('libopensync')
  
  mv $srcdir/sources/opensync $srcdir/sources/$pkgname-$pkgver
  cd $srcdir/sources/$pkgname-$pkgver
  
  #disable treating of warnings as errors
  find /$(pwd) -type f -exec sed -i 's/-Werror//g' '{}' \;
  
  mkdir build
  cd build
  cmake -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_MODULE_PATH="${srcdir}/sources/cmake-modules" \
    $srcdir/sources/$pkgname-$pkgver
  make
  make DESTDIR=$pkgdir install
  
  find $pkgdir -name \*.so  -type f -exec chrpath -d {} \;
  find $pkgdir -perm /ugo+x -type f -exec chrpath -d {} \;
}

package_osynctool(){
pkgname=('osynctool')
pkgdesc='CLI interface to OpenSync'
license=('LGPL')
depends=('libopensync=0.39')
makedepends=('libopensync=0.39')
  
  mv $srcdir/sources/osynctool $srcdir/sources/$pkgname-$pkgver
  cd $srcdir/sources/$pkgname-$pkgver
  
  mkdir build
  cd build
  cmake ../ -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_MODULE_PATH="${srcdir}/sources/cmake-modules" \
    -DCMAKE_BUILD_TYPE=Release
  make || return 1
  make DESTDIR=$pkgdir install
  install -D -m644 "$pkgdir/usr/etc/bash_completion.d/osynctool.sh"\
                   "$pkgdir/etc/bash_completion.d/osynctool"
  rm -rf "$pkgdir/usr/etc/"
}

package_libopensync-plugin-evolution3() {
pkgname=('libopensync-plugin-evolution3')
pkgdesc='Novell Evolution plugin for OpenSync'
license=('LGPL')
depends=('libopensync=0.39' 'evolution-data-server>=3')
makedepends=('libopensync=0.39')
  
  mv $srcdir/sources/evolution3 $srcdir/sources/$pkgname-$pkgver
  cd $srcdir/sources/$pkgname-$pkgver
  
  mkdir build
  cd build
  cmake ../ -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_MODULE_PATH="${srcdir}/sources/cmake-modules" \
    -DCMAKE_BUILD_TYPE=Release
  make || return 1
  make DESTDIR=$pkgdir install
}

package_libopensync-plugin-file() {
pkgname=('libopensync-plugin-file')
pkgdesc='File plugin for OpenSync'
license=('LGPL')
depends=('libopensync=0.39')
makedepends=('libopensync=0.39')
conflicts=('libopensync-plugin-file-unstable')
replaces=('libopensync-plugin-file-unstable')
provides=('libopensync-plugin-file=0.39')
  
  mv $srcdir/sources/file-sync $srcdir/sources/$pkgname-$pkgver
  cd $srcdir/sources/$pkgname-$pkgver
  
  mkdir build
  cd build
  cmake ../ -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_MODULE_PATH="${srcdir}/sources/cmake-modules" \
    -DCMAKE_BUILD_TYPE=Release
  make || return 1
  make DESTDIR=$pkgdir install
}

package_libopensync-plugin-google-calendar() {
pkgname=('libopensync-plugin-google-calendar')
pkgdesc='Google Calendar plugin for OpenSync'
license=('GPL')
depends=('libopensync=0.39' 'libgcal')
makedepends=('libopensync=0.39')
replaces=('libopensync-plugin-gcalendar')
  
  mv $srcdir/sources/google-calendar $srcdir/sources/$pkgname-$pkgver
  cd $srcdir/sources/$pkgname-$pkgver
  
  mkdir build
  cd build
  cmake ../ -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_MODULE_PATH="${srcdir}/sources/cmake-modules" \
    -DCMAKE_BUILD_TYPE=Release
  make || return 1
  make DESTDIR=$startdir/pkg install || return 1
}

package_libopensync-plugin-vformat() {
pkgname=('libopensync-plugin-vformat')
pkgdesc='vformat plugin for OpenSync'
license=('LGPL')
depends=('libopensync=0.39')
makedepends=('libopensync=0.39')
  
  mv $srcdir/sources/vformat $srcdir/sources/$pkgname-$pkgver
  cd $srcdir/sources/$pkgname-$pkgver
  
  mkdir build
  cd build
  cmake ../ -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_MODULE_PATH="${srcdir}/sources/cmake-modules" \
    -DCMAKE_BUILD_TYPE=Release
  make || return 1
  make DESTDIR=$pkgdir install
}

package_libopensync-plugin-xmlformat() {
pkgname=('libopensync-plugin-xmlformat')
pkgdesc='XML format plugin for OpenSync'
license=('LGPL')
depends=('libopensync=0.39')
makedepends=('libopensync=0.39')
  
  mv $srcdir/sources/xmlformat $srcdir/sources/$pkgname-$pkgver
  cd $srcdir/sources/$pkgname-$pkgver
  
  mkdir build
  cd build
  cmake ../ -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_MODULE_PATH="${srcdir}/sources/cmake-modules" \
    -DCMAKE_BUILD_TYPE=Release
  make || return 1
  make DESTDIR=$pkgdir install
}

pkgname=('libopensync4x-barry')
pkgdesc="Barry snapshot of the OpenSync 0.4x synchronisation framework. It also builds most of the OpenSync plugins for compatibility."