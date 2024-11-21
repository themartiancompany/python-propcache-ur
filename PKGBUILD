# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Truocolo <truocolo@aol.com>

_offline="false"
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
pkgver=0.2.1
_commit="726b8989e792a463d1eed8ded51128d457736a93"
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
# _ns="aio-libs"
_ns="themartiancompany"
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
  "${_py}-flit-core"
  "${_py}-installer"
  "${_py}-poetry-core"
  "${_py}-pyproject-hooks"
  "${_py}-setuptools"
  "${_py}-sphinx"
  "${_py}-tomli"
  "towncrier"
)
checkdepends=(
  "${_py}-pytest"
)
_tag_name="commit"
# _tag_name="tag"
_tag="${_commit}"
# _tag="v${pkgver}"
_src="git+${url}.git#${_tag_name}=${_tag}"
if [[ "${_offline}" == true ]]; then
  _src="git+file://${HOME}/${_pkg}#${_tag_name}=${_tag}"
fi
source=(
  "${_src}"
)
sha512sums=(
  'SKIP'
)

build() {
  cd \
    "${_pkg}"
  # export \
  #   PYTHONPATH="$(pwd)/packaging:$(pwd)/packaging/pep517_backend:${PYTHONPATH}"
  # cp \
  #   -r \
  #   'packaging/pep517_backend/'* \
  #   "packaging"
  # PYTHONPATH="$(pwd)/packaging:${PYTHONPATH}" \
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
