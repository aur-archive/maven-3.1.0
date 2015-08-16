# $Id$
# Maintainer: Leonidas Spyropoulos <artafinde at gmail dot com>
# Based on https://projects.archlinux.org/svntogit/community.git/tree/trunk/PKGBUILD?h=packages/maven
# Note: Temporary updated version until the official repositories update to 3.1.0

pkgname=maven-3.1.0
pkgver=3.1.0
pkgrel=1
pkgdesc="A Java project management and project comprehension tool"
arch=('any')
url="http://maven.apache.org"
license=('APACHE')
depends=('java-environment')
makedepends=('apache-ant')
conflicts=('maven')
provides=('maven')
backup=('opt/maven/conf/settings.xml')
source=(http://apache-mirror.rbc.ru/pub/apache/maven/maven-3/$pkgver/source/apache-maven-$pkgver-src.tar.gz
	maven.sh)
md5sums=('6c1acfb942763cf190eb5ce3742f6ba3'
         '5ed0bddbf5c5375fe5032a76a9506426')

package() {
  cd $srcdir/apache-maven-$pkgver

  if [-e /etc/profile.d/jre.sh ]
  then
      . /etc/profile.d/jre.sh
  else
      . /etc/profile.d/jdk.sh
  fi

  mkdir -p $srcdir/repo
  mkdir $pkgdir/opt
  export MAVEN_OPTS=-Xmx512m
  export M2_HOME=$pkgdir/opt/maven
  export PATH=$PATH:$M2_HOME/bin

  # FIXME: downloads many deps from Internet. Probably they should be
  # packaged or added into source=()
  ant -Dmaven.repo.local=$srcdir/repo
  install -D -m 755 $srcdir/maven.sh $pkgdir/etc/profile.d/maven.sh
  rm $pkgdir/opt/maven/*.txt
  mkdir -p $pkgdir/usr/bin
  ln -s /opt/maven/bin/mvn $pkgdir/usr/bin/mvn
}
