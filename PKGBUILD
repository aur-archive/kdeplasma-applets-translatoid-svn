# Contributor: Timur Antipin < kosmocap (at) gmail.com >

pkgname=kdeplasma-applets-translatoid-svn
pkgver=1339124
pkgrel=1
pkgdesc="A translator plasmoid using google translator"
arch=('i686' 'x86_64')
url="http://www.kde-look.org/content/show.php/translatoid?content=97511"
license=('LGPL')
depends=('kdebase-workspace' 'qjson')
makedepends=('cmake' 'automoc4' 'subversion')
conflicts=('translatoid-plasmoid-svn' 'kdeplasma-applets-translatoid')
replaces=('translatoid-plasmoid-svn')

_svntrunk="svn://anonsvn.kde.org/home/kde/trunk/playground/base/plasma/applets/translatoid"
_svnmod="translatoid"

build() {
  msg "Connecting to SVN server...."

  if [ -d "$_svnmod/.svn" ]; then
    (cd "$_svnmod" && svn up -r "$pkgver")
  else
    svn co "$_svntrunk" --config-dir ./ -r "$pkgver" "$_svnmod"
  fi
  
  msg "SVN checkout done or server timeout"
  msg "Starting build..."
  
  rm -rf "${srcdir}"/build
  mkdir "${srcdir}"/build
  cd "${srcdir}"/build
  cmake ../${_svnmod} \
    -DQT_QMAKE_EXECUTABLE=/usr/bin/qmake-qt4 -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_BUILD_TYPE=Release
  make
}

package(){
  cd build
  make DESTDIR="${pkgdir}" install
  rm -r $pkgdir/usr/share/apps/cmake/
}