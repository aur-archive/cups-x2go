# Maintainer: Milan Knížek <knizek@volny.cz>
pkgname=cups-x2go
pkgver=3.0.0.4
pkgrel=1
pkgdesc="CUPS-X2GO provides an X2go backend to CUPS."
arch=('i686' 'x86_64')
url="http://www.x2go.org/"
license=('GPL')
depends=('cups' 'ghostscript')
options=(emptydirs)
install=cups-x2go.install
groups=('x2go' 'alts')
source=("http://code.x2go.org/releases/source/${pkgname}/${pkgname}-${pkgver}.tar.gz")

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}"

  # prepare existing .install file for install command
  sed -i -e 's@\(^[a-Z0-9\.\-]*\)\( *\)\(.*$\)$@\1\2\3\1@g' \
         -e "s@ \([a-z]\)@ ${pkgdir}/\1@g" \
         -e 's@^@-m 644 @g' \
         -e 's@\-m 644\( cups\-x2go \)@\-m 755\1@' \
         -e '$s@$@\n@' debian/cups-x2go.install

  for dir in $(cat debian/cups-x2go.dirs); do
    install -d -m 755 "$pkgdir/$dir"
  done

  while read line; do
    install -m 644 $line
  done < debian/cups-x2go.install

  install -m 755 -d "${pkgdir}/usr/share/doc/${pkgname}"
  install -m 644 "debian/changelog" "${pkgdir}/usr/share/doc/${pkgname}/changelog.DEBIAN"
  install -m 644 "debian/copyright" "${pkgdir}/usr/share/doc/${pkgname}/copyright.DEBIAN"
}
md5sums=('290226559d2d018a4ef360e029477bc2')
