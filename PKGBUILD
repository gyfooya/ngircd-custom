# Maintainer: Kyle Keen <keenerd@gmail.com>
pkgname=ngircd
pkgver=27
pkgrel=0
pkgdesc="Next Generation IRC Daemon (without ident support)"
arch=('x86_64')
backup=('etc/ngircd.conf')
url="https://ngircd.barton.de/"
license=('GPL')
depends=('openssl' 'zlib')
source=("https://ngircd.barton.de/pub/ngircd/ngircd-$pkgver.tar.gz"
        "ngircd.service")
sha256sums=('fd38ef21339daf81d6af4a630ba3b2de51a1b42c181843ee77635a5a661fe73c'
            'SKIP')

build() {
  cd "$srcdir/$pkgname-$pkgver"

  ./configure --prefix=/usr \
      --sysconfdir=/etc \
      --sbindir=/usr/bin \
      --mandir=/usr/share/man \
      --without-ident \
      --with-openssl \
      --enable-ipv6

  make
}

package() {
  cd "$srcdir/$pkgname-$pkgver"

  make DESTDIR="$pkgdir" install
  install -Dm644 ../ngircd.service "$pkgdir/usr/lib/systemd/system/ngircd.service"
}
