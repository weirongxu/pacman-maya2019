# Maintainer ~ kyle[dot]devir[at]mykolab[dot]com
# Contributor: Luca Weiss <luca (at) z3ntu (dot) xyz>

pkgname=maya
pkgver=2019
_pkgver=2019
pkgrel=1
pkgdesc="Autodesk Maya 3D modelling software suite"
arch=('x86_64')
url="http://www.autodesk.com/products/maya/overview"
license=('custom: unlimited')
depends=('libpng12' 'tcsh' 'libxp' 'openssl' 'libjpeg6-turbo' 'libtiff' 'gamin'
         'audiofile' 'e2fsprogs' 'xorg-fonts-75dpi' 'xorg-fonts-100dpi'
         'xorg-fonts-misc' 'openssl-1.0')
install="maya.install"
options=(!strip)
source=(
# 'https://up.autodesk.com/2019/MAYA/Autodesk_Maya_2019_Linux_64bit.tgz'
'./Autodesk_Maya_2019_Linux_64bit.tgz'
'maya.desktop'
)
sha512sums=('45a247e739eceb360cdd39a763e91ada8717f5b63b976ffed0f318ff691c9e656b6b81789913b2e2792c0a58297f40393a21480b39650ea8125ad989e5b366c8'
            'f39f9e9bf11efbbbb2bf395bc869f6e1141b1fa331ac4edd7f3c1b1f9daf30854cecb24cf92395e1e75222833c5bda557bb4d4412fb5aa374ba0aeb5157b10d9')

prepare() {
    cd "$srcdir"

    rm -Rf ../maya-setup
    mkdir -p ../maya-setup
    mv * ../maya-setup
}

package() {
    cd "$pkgdir"

    # Extract RPMs
    for i in ../../maya-setup/*.rpm; do
        msg2 "Extracting ${i}"
        bsdtar -xf $i
    done

    mkdir "$pkgdir"/usr/tmp/
    chmod 777 "$pkgdir"/usr/tmp/

#    mkdir -p "$pkgdir"/usr/lib/
#    chmod 755 "$pkgdir"/usr/lib/
#    cp "$pkgdir"/opt/Autodesk/Adlm/R12/lib64/libadlmPIT.so.12  "$pkgdir"/usr/lib/libadlmPIT.so.12
#    cp "$pkgdir"/opt/Autodesk/Adlm/R12/lib64/libadlmutil.so.12 "$pkgdir"/usr/lib/libadlmutil.so.12

    ln -s /usr/lib/libssl.so.1.0.0 "$pkgdir"/usr/autodesk/maya2019/lib/libssl.so.10
    ln -s /usr/lib/libcrypto.so.1.0.0 "$pkgdir"/usr/autodesk/maya2019/lib/libcrypto.so.10
    ln -s /usr/lib/libjpeg.so.62 "$pkgdir"/usr/autodesk/maya2019/lib/libjpeg.so.62
    ln -s /usr/lib/libtiff.so "$pkgdir"/usr/autodesk/maya2019/lib/libtiff.so.3

    mkdir -p "$pkgdir"/usr/bin/
    chmod 755 "$pkgdir"/usr/bin/
    ln -s /usr/autodesk/maya2019/bin/maya2019 "$pkgdir"/usr/bin/maya2019

    mkdir -p "$pkgdir"/usr/share/applications/
    chmod 755 "$pkgdir"/usr/share/applications/
    install -Dm644 ../../maya-setup/maya.desktop "$pkgdir"/usr/share/applications/maya.desktop

    mkdir -p "$pkgdir"/opt/maya-setup/
    chmod 755 "$pkgdir"/opt/maya-setup/
    cp ../../maya-setup/setup{,.xml} "$pkgdir"/opt/maya-setup/
}
