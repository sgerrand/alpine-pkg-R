# Contributor: Sasha Gerrand <alpine-pkg-R@sgerrand.com>
# Maintainer: Sasha Gerrand <alpine-pkg-R@sgerrand.com>
pkgname=R
pkgver=3.3.0
pkgrel=0
pkgdesc="R is a system for statistical computation and graphics"
url="https://www.r-project.org"
arch="all"
license="GPL2"
depends=""
depends_dev="bzip2-dev ca-certificates curl-dev pcre-dev perl readline-dev xz-dev zlib-dev"
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
		--enable-utf8 \
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

md5sums="5a7506c8813432d1621c9725e86baf7a  R-3.3.0.tar.gz
4368a6983cf584d666c51aa61d680209  10-glibc-disable-stack-end.patch"
sha256sums="9256b154b1a5993d844bee7b1955cd49c99ad72cef03cce3cd1bdca1310311e4  R-3.3.0.tar.gz
26a00af590550a19d6a2c3e21ce932de6722300d1dd18729bdfa16b57da23242  10-glibc-disable-stack-end.patch"
sha512sums="81e9ef761bee4d9322ca785fbed843ab13c2f5b55be769d982a81a7e7694e03980cbc7ee067fc850bd7a17ab65d93be81f27db50d428665773174c690383d4cc  R-3.3.0.tar.gz
a1b3d9ad70dc77a649f0b56e1080e2f833e7eba23408ee710d372bfde06eb651418c78f640554743666c812eb0d268e0db48b2cbf038481c9ede46e4d4f43c3e  10-glibc-disable-stack-end.patch"
