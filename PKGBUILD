# Maintainer: Cp Dong <cp-dong at outlook dot com>

pkgname=slstatus
pkgver=1.0
pkgrel=2
pkgdesc='A status monitor for window managers that use WM_NAME or stdin to fill the status bar'
arch=(any)
url='http://tools.suckless.org/slstatus/'
depends=('libx11' 'alsa-utils')
conflicts=('slstatus-git')
license=('custom:ISC')
source=('https://dl.suckless.org/tools/slstatus-1.0.tar.gz' 'https://tools.suckless.org/slstatus/patches/alsa-master/slstatus-alsa-master-20230420-84a2f11.diff'
        'config.h')
sha256sums=('6d6d0a16c08dd9d211172c30c4720701267a3f40cdc938db3f386f6a2b6cff54'
            '922b8bc4e69b30060abb6417574112eaeca43e2e5248ac8a4ce14295d50304f3'
            'SKIP')

prepare() {
    cd "$srcdir/$pkgname-$pkgver"
    if [[ ! -f "$srcdir/$pkgname-$pkgver/components/alsa_master_vol.c" ]]; then
        patch --forward --strip=1 --input=../slstatus-alsa-master-20230420-84a2f11.diff
    fi
    if [[ -f "$srcdir/config.h" ]]; then
        cp -fv "$srcdir/config.h" config.h
    fi
}

build() {
    cd "$srcdir/$pkgname-$pkgver"
    make X11INC='/usr/include/X11' X11LIB='/usr/lib/X11' CFLAGS='-fpermissive'
}

package() {
    cd "$srcdir/$pkgname-$pkgver"
    install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/$pkgname/LICENSE"
    make PREFIX='/usr' DESTDIR="${pkgdir}" install
}
