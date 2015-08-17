# $Id: PKGBUILD 156994 2012-04-23 09:10:49Z ibiru $
# Maintainer: Ionut Biru <ibiru@archlinux.org>
#
#	Custom AUR Package Maintainer: Diogo B. <db_eee.at.hotmail.dot.com>

pkgname=udisks2-systemd
pkgver=1.97.0
pkgrel=1
pkgdesc="Disk Management Service, version 2. Native systemd support."
arch=('i686' 'x86_64')
url="http://www.freedesktop.org/wiki/Software/udisks"
license=('GPL2')
depends=('glib2' 'udev' 'polkit-systemd' 'libatasmart' 'eject' 'systemd')
makedepends=('intltool' 'docbook-xsl' 'gobject-introspection')
optdepends=('parted: partition management'
            'gptfdisk: GUID partition table support')
provides=('udisks2=1.97.0')
conflicts=('udisks2')
options=(!libtool)
source=(http://udisks.freedesktop.org/releases/udisks-${pkgver}.tar.bz2
	55-myconf.pkla)

sha256sums=('132e569d1b565a74c481d37ba27977c9aa9f5254baf79b2763898c9fa35a4ceb'
            '52924d7d1bacb8eba0aeda569924250c941b7a61a25239252ef4dc1e4ca55df5')

build() {
  cd "udisks-$pkgver"
  ./configure --prefix=/usr --sysconfdir=/etc \
      --with-systemdsystemunitdir=/usr/lib/systemd/system \
      --localstatedir=/var --disable-static
  make
}

package() {
  cd "udisks-$pkgver"
  make DESTDIR="$pkgdir" install
  
  # Mount without password!
  mkdir "${pkgdir}/etc/polkit-1/"
  mkdir "${pkgdir}/etc/polkit-1/localauthority/"
  mkdir "${pkgdir}/etc/polkit-1/localauthority/50-local.d"
  install -m 644 "${srcdir}/55-myconf.pkla" "${pkgdir}/etc/polkit-1/localauthority/50-local.d/"
}
