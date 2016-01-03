# Contributor: Sasha Gerrand <alpine-pkg-R@sgerrand.com>
# Maintainer: Sasha Gerrand <alpine-pkg-R@sgerrand.com>
pkgname=R
pkgver=3.2.3
pkgrel=0
pkgdesc="R is a system for statistical computation and graphics"
url="https://www.r-project.org"
arch="all"
license="GPL2"
depends=""
depends_dev="$pkgname pcre-dev perl readline-dev"
makedepends="$depends_dev autoconf automake gfortran"
install=""
subpackages="$pkgname-dev $pkgname-doc"
source="https://cran.rstudio.com/src/base/R-3/R-$pkgver.tar.gz
        glibc-0001-disable-stack-end.patch"

_builddir="$srcdir/$pkgname-$pkgver"

prepare() {
	cd "$_builddir"
	for i in $source; do
		case $i in
		glibc-*.patch)
			msg "Applying ${i}"; patch -p2 -i "$srcdir/$i" || return 1;;
		esac
	done
}

build() {
	cd "$_builddir"
	./configure \
		--build=$CBUILD \
		--host=$CHOST \
		--prefix=/usr \
		--sysconfdir=/etc \
		--mandir=/usr/share/man \
		--localstatedir=/var \
		--disable-java \
		--without-x \
		|| return 1
	make || return 1
}

package() {
	cd "$_builddir"
	make DESTDIR="$pkgdir" install || return 1
}

dev() {
	default_dev || return 1
}

doc() {
	default_doc || return 1
	cd "$srcdir/$pkgname-$pkgver"
	_docs="COPYING INSTALL README"
	for _doc in $_docs; do
		install -Dm644 "$srcdir/$pkgname-$pkgver/$_doc" \
			"$subpkgdir/usr/share/doc/$pkgname/$_doc" || return 1
	done
}

md5sums="e08cf33ce894ba9b3ac1fb8e9123a51f  glibc-0001-disable-stack-end.patch
1ba3dac113efab69e706902810cc2970  R-3.2.3.tar.gz"
sha256sums="0a9497000dcb09abe9b72610b99629278e03e9167ae4a964916e08852ca774a5  glibc-0001-disable-stack-end.patch
b93b7d878138279234160f007cb9b7f81b8a72c012a15566e9ec5395cfd9b6c1  R-3.2.3.tar.gz"
sha512sums="eb998805149137e18b2e5c8213e649aaa85b5076d9fbf744cc9a7544b9dc47bc51bbf470b18577c3a10430293ea58c3b056ffe6153c47716b868100cf6e2a95a  glibc-0001-disable-stack-end.patch
9d7294af860204f4d84e25eb503111c9607beedbc42f01de073c915945a6342c3e24e25a9cc038a2e58442036bee931975d93dc327081ed02afe5ffa365170ea  R-3.2.3.tar.gz"
