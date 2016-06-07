# Contributor: Sasha Gerrand <alpine-pkg-R@sgerrand.com>
# Maintainer: Sasha Gerrand <alpine-pkg-R@sgerrand.com>
pkgname=R
pkgver=3.2.3
pkgrel=1
pkgdesc="R is a system for statistical computation and graphics"
url="https://www.r-project.org"
arch="all"
license="GPL2"
depends=""
depends_dev="pcre-dev perl readline-dev"
makedepends="$depends_dev autoconf automake gfortran"
install=""
subpackages="$pkgname-dev $pkgname-doc"
source="https://cran.rstudio.com/src/base/$pkgname-${pkgver:0:1}/$pkgname-$pkgver.tar.gz
        10-glibc-disable-stack-end.patch"

_builddir="$srcdir/$pkgname-$pkgver"

prepare() {
	cd "$_builddir"
	for i in $source; do
		case $i in
		*.patch)
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

md5sums="1ba3dac113efab69e706902810cc2970  R-3.2.3.tar.gz
4368a6983cf584d666c51aa61d680209  10-glibc-disable-stack-end.patch"
sha256sums="b93b7d878138279234160f007cb9b7f81b8a72c012a15566e9ec5395cfd9b6c1  R-3.2.3.tar.gz
26a00af590550a19d6a2c3e21ce932de6722300d1dd18729bdfa16b57da23242  10-glibc-disable-stack-end.patch"
sha512sums="9d7294af860204f4d84e25eb503111c9607beedbc42f01de073c915945a6342c3e24e25a9cc038a2e58442036bee931975d93dc327081ed02afe5ffa365170ea  R-3.2.3.tar.gz
a1b3d9ad70dc77a649f0b56e1080e2f833e7eba23408ee710d372bfde06eb651418c78f640554743666c812eb0d268e0db48b2cbf038481c9ede46e4d4f43c3e  10-glibc-disable-stack-end.patch"
