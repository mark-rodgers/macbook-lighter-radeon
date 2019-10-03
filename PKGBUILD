# Maintainer: harttle <yangjvn@126.com>
# Inspired by lighter, many thanks to Janhouse's perl script https://github.com/Janhouse/lighter
pkgname=macbook-lighter-radeon
pkgver=v0.0.2.8.gfad9e95
pkgrel=1
pkgdesc="Macbook screen/keyboard backlight CLI and auto-adjust on ambient light for Radeon GPUs"
arch=(any)
url="https://github.com/mark-rodgers/macbook-lighter-radeon"
license=('GPL')
depends=('bc')
makedepends=('git')
provides=()
conflicts=()
source=('git+https://github.com/mark-rodgers/macbook-lighter-radeon.git')
md5sums=('SKIP')

pkgver() {
  cd "$srcdir/$pkgname"
  git describe --tags | sed 's|-|.|g'
}

package() {
  cd "$srcdir/$pkgname"
  [ ! -f $pkgdir/etc/macbook-lighter-radeon.conf ] && install -Dm644 macbook-lighter-radeon.conf $pkgdir/etc/macbook-lighter-radeon.conf
  install -Dm644 "macbook-lighter-radeon.service" "$pkgdir/usr/lib/systemd/system/macbook-lighter-radeon.service"
  install -Dm755 "src/macbook-lighter-ambient.sh" "$pkgdir/usr/bin/macbook-lighter-ambient"
  install -Dm755 "src/macbook-lighter-screen.sh" "$pkgdir/usr/bin/macbook-lighter-screen"
  install -Dm755 "src/macbook-lighter-kbd.sh" "$pkgdir/usr/bin/macbook-lighter-kbd"
}
