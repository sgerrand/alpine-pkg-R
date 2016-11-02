# Contributor: Sasha Gerrand <alpine-pkg-R@sgerrand.com>
# Maintainer: Sasha Gerrand <alpine-pkg-R@sgerrand.com>
pkgname=R
pkgver=3.3.1
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
        10-glibc-disable-stack-end.patch
        20-add-aix-to-r-extra-cpp-flags.patch"

_builddir="$srcdir/$pkgname-$pkgver"

prepare() {
	cd "$_builddir"
	for i in $source; do
		case $i in
		*.patch)
			msg "Applying ${i}"; patch -p1 -i "$srcdir/$i" || return 1;;
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
		--enable-R-static-lib \
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

md5sums="f50a659738b73036e2f5635adbd229c5  R-3.3.1.tar.gz
5e221346d92824dd33d328054942b505  10-glibc-disable-stack-end.patch
8cab50c334cc4bbd9cdbddb3ea910eca  20-add-aix-to-r-extra-cpp-flags.patch"
sha256sums="3dc59ae5831f5380f83c169bac2103ad052efe0ecec4ffa74bde4d85a0fda9e2  R-3.3.1.tar.gz
d588a5d4db1ec83277221f5f0c1605110a0d46cd2abb567f744ad83f35da3c40  10-glibc-disable-stack-end.patch
ca142e4dad1694550fe462540ee5feef3687a1f16c6e970e186cf0dc0b2f3704  20-add-aix-to-r-extra-cpp-flags.patch"
sha512sums="d0ff85e99b9ec9cac672aa30d7d1a854778c6a610bcc5336e8c60c8c74f20856f2bfeae085af793fad646ff45cb4677d9d6dcbaa18212591f72f00a02339f4cd  R-3.3.1.tar.gz
f5e72f742a540c1a5439221ca1afcd1d2c0f4421dac6f2301231ce4905bdf12a4b6cab7213f15849d3f9f4d0bd6addc91ef8805213dad23794245f7ea12aa102  10-glibc-disable-stack-end.patch
658c8c47baeb4914ccc8deec34d4f4229933134ff189724349201fe0768115b70d74af60bf54fb9e692951b70ca7458450e1077aea5ebf5c4571b8e8afc581b9  20-add-aix-to-r-extra-cpp-flags.patch"
