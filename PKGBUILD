# Maintainer: Your Name <you@example.com>

pkgname=ngircd
pkgver=27
pkgrel=1
pkgdesc="Next Generation IRC Daemon (without ident support)"
arch=('x86_64')
url="https://ngircd.barton.de/"
license=('GPL')
depends=('openssl' 'zlib')
backup=('etc/ngircd.conf')

source=("https://ngircd.barton.de/pub/ngircd/ngircd-${pkgver}.tar.gz"{,.sig}
        ngircd.service)

sha256sums=('fd38ef21339daf81d6af4a630ba3b2de51a1b42c181843ee77635a5a661fe73c'
            'SKIP'
            'da49e396c77a0632324cab7a887562367178f8ff103cbaa8f3fef080b66cfb7b')

validpgpkeys=('5F22A309911C1C6EFA1B69C1FE8B05CE1FA6365E') # Alexander Barton

build() {
  cd "$srcdir/$pkgname-$pkgver"

  ./configure \
    --prefix=/usr \
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

  install -Dm644 "$srcdir/ngircd.service" \
    "$pkgdir/usr/lib/systemd/system/ngircd.service"
}
