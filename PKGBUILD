# Original Author: Squalou Jenkins  <squalou.jenkins at gmail dot com>
# Maintainer: Squalou Jenkins  <squalou.jenkins at gmail dot com>

pkgname=xbmc-pi-manager
pkgver=20130806
pkgrel=2
pkgdesc="scripts to start/stop xbmc depending on HDMI status on Raspberry Pi"
arch=('any')
url="https://github.com/squalou/xbmcmanager"
license=('GPL2')
depends=('xbmc' 'raspberrypi-firmware-tools' 'bash' 'sudo')
install='xbmc-pi-manager.install'


_gitroot=https://github.com/squalou/xbmcmanager.git
_gitname=$pkgname-$pkgver


build() {

   msg "Connecting to GIT server...."

   if [[ -d "$_gitname" ]]; then
     cd "$_gitname" && git pull
     msg "The local files are updated."
   else
     msg "Getting a fresh clone..."
     git clone $_gitroot $_gitname
     cd $_gitname
   fi

   msg "GIT checkout done or server timeout"
   
}

package() {
   mkdir -p "$pkgdir/usr/lib/systemd/system/"
   mkdir -m750 -p "$pkgdir/etc/sudoers.d/"
   mkdir -p "$pkgdir/etc/conf.d/"
   mkdir -p "$pkgdir/usr/bin/"

   install -v -m 644 -t "$pkgdir/usr/lib/systemd/system/" $srcdir/$_gitname/src/xbmc-pi-manager/systemd/xbmcmanager.service
   install -v -m 644 -t "$pkgdir/etc/sudoers.d/" $srcdir/$_gitname/src/xbmc-pi-manager/sudoers.d/xbmcmanager
   install -v -m 644 -t "$pkgdir/etc/conf.d/" $srcdir/$_gitname/src/xbmc-pi-manager/conf.d/xbmcmanager
   install -v -m 755 -t "$pkgdir/usr/bin/" $srcdir/$_gitname/src/xbmc-pi-manager/bin/xbmc.start
   install -v -m 755 -t "$pkgdir/usr/bin/" $srcdir/$_gitname/src/xbmc-pi-manager/bin/xbmc.stop
   install -v -m 755 -t "$pkgdir/usr/bin/" $srcdir/$_gitname/src/xbmc-pi-manager/bin/xbmcmanager.sh

}
