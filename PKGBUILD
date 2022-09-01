#!/bin/bash

# Built from the original AUR package by Daniel Bermond <dbermond@archlinux.org>

# Disable various shellcheck rules that produce false positives in this file.
# Repository rules should be added to the .shellcheckrc file located in the
# repository root directory, see https://github.com/koalaman/shellcheck/wiki
# and https://archiv8.github.io for further information.
# shellcheck disable=SC2034,SC2154
# [ToDo]: Add files: User documentation
# [ToDo]: Add files: Tooling
# [FixMe]: Namcap warnings and errors

# Maintainer: Ross Clark <https://github.com/Archiv8/celt/discussions>
# Contributor: Ross Clark <https://github.com/Archiv8/celt/discussions>

pkgname=celt
pkgver=0.11.3
pkgrel=5
pkgdesc='Low-latency audio communication codec'
arch=('x86_64')
url='https://gitlab.xiph.org/xiph/celt/'
license=('BSD')
depends=(
  'libogg'
  )
source=("https://gitlab.xiph.org/xiph/celt/-/archive/v${pkgver}/celt-v${pkgver}.tar.bz2"
        '010-celt-fix-tandem-test.patch'::'https://gitlab.xiph.org/xiph/celt/-/commit/c5f999097f64eb090e1a353a57f80045ece7330a.patch')
sha256sums=('e11a3ff390a733a470ca3ceb1f74c19770ee7c6f0ee169fdebc7b6efdc8700be'
            '2d8fa7454dfbc3136ea361123a2793d49a56eccdd9042c6d99364bdd29e9d484')

prepare() {
    patch -d "${pkgname}-v${pkgver}" -Np1 -i "${srcdir}/010-celt-fix-tandem-test.patch"
    "${pkgname}-v${pkgver}/autogen.sh"
}

build() {
    cd "${pkgname}-v${pkgver}"
    ./configure --prefix='/usr' --enable-custom-modes
    make
}

check() {
    make -C "${pkgname}-v${pkgver}" check
}

package() {
    make -C "${pkgname}-v${pkgver}" DESTDIR="$pkgdir" install
    install -D -m644 "${pkgname}-v${pkgver}/COPYING" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
