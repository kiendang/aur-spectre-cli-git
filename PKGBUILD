# Maintainer: Kien Dang <mail at kien dot ai>

_binname=spectre
_pkgname="${_binname}-cli"
pkgname="${_pkgname}-git"
pkgver=2.6.cli.5.r114.a5e7aab
pkgrel=1
pkgdesc='CLI tool for the Spectre password cypher'
arch=('x86_64')
url='https://spectre.app'
license=('GPL3')
depends=(libsodium json-c)
makedepends=(git cmake ncurses)
provides=("${_pkgname}")
conflicts=("${_pkgname}")
options=()
install=
source=("${_pkgname}::git+https://gitlab.com/spectre.app/cli.git"
        "${_binname}-api::git+https://gitlab.com/spectre.app/api.git")
sha256sums=('SKIP'
            'SKIP')

_srcdir="${_pkgname}"

pkgver() {
  cd "${_srcdir}"
  printf "%s" "$(git describe --match '*-cli*' --long --dirty | sed 's/\([^-]*-\)g/r\1/;s/-/./g')"
  # printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
  cd "${_srcdir}"
  git submodule init
  git config submodule.api.url "../${_binname}-api"
  git submodule update
}

build() {
  cd "${_srcdir}"
  cmake .
  make
}

package() {
  cd "${_srcdir}"
  install -D -m755 "${_binname}" "${pkgdir}/usr/bin/${_binname}"
  install -D -m644 "LICENSE" "${pkgdir}/usr/share/licenses/${_binname}/LICENSE"
  install -D -m644 "${_binname}.completion.bash" "${pkgdir}/usr/share/bash-completion/completions/spectre"
}
