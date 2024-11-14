# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Truocolo <truocolo@aol.com>

_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
_pkg=propcache
pkgname="${_py}-${_pkg}"
pkgver=0.2
# _commit=1e2f6f9cac5cc60f0adab051c14adf09ffe39155
pkgrel=1
_pkgdesc=(
  "Fast implementation of cached"
  "properties for Python 3.8+"
)
arch=(
  'any'
)
license=(
  'Apache-2.0'
)
_http="https://github.com"
_ns="aio-libs"
url="${_http}/${_ns}/${_pkg}"
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
)
makedepends=(
  'git'
  "cython"
  "${_py}-build"
  "${_py}-expandvars"
  "${_py}-installer"
  "${_py}-setuptools"
  "${_py}-sphinx"
  "${_py}-tomli"
  "towncrier"
)
checkdepends=(
  "${_py}-pytest"
)
source=(
  "git+${url}.git#tag=${pkgver}"
)
sha512sums=(
  'SKIP'
)

build() {
  cd \
    "${_pkg}"
  "${_py}" \
    -m \
      build \
    -nw
}

check() {
  cd \
    "${_pkg}"
  "${_py}" \
    -m installer
    --destdir=tmp_install \
    dist/*.whl
  # I am starting to think we should generate
  # python packages automatically
  PYTHONPATH="$PWD/tmp_install/usr/lib/python${_pymajver}/site-packages" \
  pytest
}

package() {
  cd \
    "${_pkg}"
  "${_py}" \
    -m installer \
    --destdir="${pkgdir}" \
    dist/*.whl
  install \
    -Dm644 \
    LICENSE \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgname}/"
}

# vim:set sw=2 sts=-1 et:
