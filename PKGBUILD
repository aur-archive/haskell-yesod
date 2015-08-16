# Maintainer: Olaf Leidinger <oleid@mescharet.de>
_hkgname=yesod
pkgname=haskell-yesod
pkgver=1.2.5.2
pkgrel=1
pkgdesc="Creation of type-safe, RESTful web applications."
url="http://hackage.haskell.org/package/${_hkgname}"
license=('custom:MIT')
arch=('i686' 'x86_64')
makedepends=()
depends=('ghc' 'haskell-aeson' 'haskell-blaze-html>=0.5' 'haskell-blaze-markup>=0.5.1' 'haskell-bytestring' 'haskell-data-default' 'haskell-directory' 'haskell-hamlet<1.2' 'haskell-monad-control<0.4' 'haskell-network-conduit' 'haskell-safe' 'haskell-shakespeare-css<1.1' 'haskell-shakespeare-js<1.3' 'haskell-template-haskell' 'haskell-text' 'haskell-transformers' 'haskell-unix' 'haskell-unordered-containers' 'haskell-wai' 'haskell-wai-extra' 'haskell-warp' 'haskell-yaml' 'haskell-yesod-auth<1.3' 'haskell-yesod-core<1.3' 'haskell-yesod-form<1.4' 'haskell-yesod-persistent<1.3')
options=('strip')
source=(http://hackage.haskell.org/packages/archive/${_hkgname}/${pkgver}/${_hkgname}-${pkgver}.tar.gz)
install=${pkgname}.install
md5sums=('9a19661d3a1c5ab99f5cc3b7424e6259')
build() {
    cd ${srcdir}/${_hkgname}-${pkgver}
    runhaskell Setup configure -O ${PKGBUILD_HASKELL_ENABLE_PROFILING:+-p } --enable-split-objs --enable-shared \
       --prefix=/usr --docdir=/usr/share/doc/${pkgname} --libsubdir=\$compiler/site-local/\$pkgid
    runhaskell Setup build
    runhaskell Setup haddock
    runhaskell Setup register   --gen-script
    runhaskell Setup unregister --gen-script
    sed -i -r -e "s|ghc-pkg.*unregister[^ ]* |&'--force' |" unregister.sh
}
package() {
    cd ${srcdir}/${_hkgname}-${pkgver}
    install -D -m744 register.sh   ${pkgdir}/usr/share/haskell/${pkgname}/register.sh
    install    -m744 unregister.sh ${pkgdir}/usr/share/haskell/${pkgname}/unregister.sh
    install -d -m755 ${pkgdir}/usr/share/doc/ghc/html/libraries
    ln -s /usr/share/doc/${pkgname}/html ${pkgdir}/usr/share/doc/ghc/html/libraries/${_hkgname}
    runhaskell Setup copy --destdir=${pkgdir}
    install -D -m644 LICENSE ${pkgdir}/usr/share/licenses/${pkgname}/LICENSE
    rm -f ${pkgdir}/usr/share/doc/${pkgname}/LICENSE
}
