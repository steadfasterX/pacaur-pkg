pkgname=pacaur
pkgver=9.9.9
pkgrel=1
pkgdesc="An AUR helper that minimizes user interaction"
arch=('any')
url="https://github.com/steadfasterX/pacaur"
license=('ISC')
depends=('cower' 'expac' 'sudo' 'git')
makedepends=('perl')
backup=('etc/xdg/pacaur/config')
source=("https://github.com/steadfasterX/$pkgname/archive/$pkgver.tar.gz")
md5sums=('9dc63349b5897eeeb6b73ef07a15b1e9')

build() {
    cd "arch_$pkgname-$pkgver"
    pod2man --utf8 --section=8 --center="Pacaur Manual" --name="PACAUR"\
        --release="$pkgname $pkgver" ./README.pod > ./pacaur.8
}

package() {
    cd "arch_$pkgname-$pkgver"

    mkdir -p "$pkgdir/etc/xdg/pacaur"
    install -D -m644 ./config "$pkgdir/etc/xdg/pacaur/config"
    mkdir -p "$pkgdir/usr/bin"
    install -D -m755 ./pacaur "$pkgdir/usr/bin/$pkgname"
    mkdir -p "$pkgdir/usr/share/bash-completion/completions"
    install -D -m644 ./bash.completion\
        "$pkgdir/usr/share/bash-completion/completions/$pkgname"
    mkdir -p "$pkgdir/usr/share/zsh/site-functions"
    install -D -m644 ./zsh.completion\
        "$pkgdir/usr/share/zsh/site-functions/_pacaur"
    mkdir -p "$pkgdir/usr/share/man/man8"
    install -D -m644 ./pacaur.8 "$pkgdir/usr/share/man/man8/pacaur.8"
    mkdir -p "$pkgdir/usr/share/licenses/pacaur"
    install -D -m644 ./LICENSE "$pkgdir/usr/share/licenses/pacaur/LICENSE"
    for i in {ca,da,de,es,fi,fr,hu,it,ja,nb,nl,pl,pt,ru,sk,sl,sr,sr@latin,tr,zh_CN}; do
        mkdir -p "$pkgdir/usr/share/locale/$i/LC_MESSAGES/"
        msgfmt ./po/$i.po -o "$pkgdir/usr/share/locale/$i/LC_MESSAGES/pacaur.mo"
    done
}

