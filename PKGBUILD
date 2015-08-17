# Contributor:  Elder Marco <eldermarco at gmail dot com>
# Maintainer: Isay Humberto <iLudeZ25 at gmail dot com>
pkgname=seismicunix
_pkgname=cwp_su_all
pkgver=43R6
pkgrel=7
pkgdesc="Open source software for seismic research and seismic processing"
license=('BSD')
url="http://www.cwp.mines.edu/cwpcodes/"
source=("ftp://ftp.cwp.mines.edu/pub/cwpcodes/${_pkgname}_${pkgver}.tgz"
        "$pkgname-$pkgver-makefile-config.patch"
        "$pkgname-$pkgver-no-questions.patch"
        "$pkgname.sh"
        "$pkgname.csh")

makedepends=('ed' 'libxmu' 'libxi' 'mesa' 'freeglut' 'lesstif' 'gcc-fortran')
depends=('libxmu' 'libxi' 'mesa' 'freeglut' 'lesstif')

arch=('i686' 'x86_64')
md5sums=('1e005d058804c735bd520cbce7437f0f'
         '2817e81b092550d0b61beb3eeeba5bf0'
         '24d267f1afe03ed7a5ef074e1b7bbc57'
         '0c2d9ce30ab3067b5eb1caebc2b2ef88'
         '25e78ccdba76eb5e2cb5fc125c1c5504')

build () {
    cd "$srcdir/src"
    patch -Np1 -i ../$pkgname-$pkgver-makefile-config.patch
    patch -Np1 -i ../$pkgname-$pkgver-no-questions.patch
    export CWPROOT="$srcdir"

    # These codes are essential. Please, don't change anything
    # below.
    make -j1 install        # Basic set of code
    make -j1 xtinstall      # X-toolkit applications

    # The rest are nonessential. You can comment these lines, if
    # you want.
    make -j1 finstall       # Fortran codes
    make -j1 mglinstall     # Mesa/OpenGL items
    make -j1 xminstall      # Motif application
    make -j1 sfinstall      # Sfio materials and SEGDREAD
    make -j1 utils          # libcwputils
}

package () {
    cd "$srcdir"

    # Binary files
    mkdir -p "$pkgdir/opt/$pkgname/bin"
    cp -pr bin/* "$pkgdir/opt/$pkgname/bin/"

    # Include Headers
    mkdir -p "$pkgdir/opt/$pkgname/include"
    cp -pr include/* "$pkgdir/opt/$pkgname/include/"

    # Libraries
    mkdir -p "$pkgdir/opt/$pkgname/lib/"
    cp -pr lib/* "$pkgdir/opt/$pkgname/lib/"

    # Source Code and others
    mkdir -p "$pkgdir/opt/$pkgname/src"
    find src/*  -maxdepth 0 -type d -exec cp -pr '{}' "$pkgdir/opt/$pkgname/src/" \;
    rm -rf "$pkgname/opt/$pkgname/src/configs" \
           "$pkgname/opt/$pkgname/src/Portability"

    # Environment Variables
    install -d -m755 "$pkgdir/etc/profile.d"
    install -m755 "${pkgname}.sh" "$pkgdir/etc/profile.d/"
    install -m755 "${pkgname}.csh" "$pkgdir/etc/profile.d/"

    # License file and acknowledgements
    install -d -m755 "$pkgdir/usr/share/licenses/$pkgname"
    install -p -m644 src/LEGAL_STATEMENT  \
        "$pkgdir/usr/share/licenses/$pkgname/COPYING"
    install -p -m644 src/ACKNOWLEDGEMENTS \
        "$pkgdir/usr/share/licenses/$pkgname/"
}
# expandtab:tabstop=4:shiftwidth=4
