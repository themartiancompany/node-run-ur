# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>

_offline="false"
_git="false"
_solc="true"
_hardhat="false"
_proj="hip"
_pkg=evmfs
pkgname="${_pkg}"
pkgver="0.0.0.0.0.0.0.0.0.1.1.1.1.1.1"
_commit="00f349cc9e12c98bd6e94e84c1276dc2fad640a8"
pkgrel=1
_pkgdesc=(
  "Ethereum Virtual Machine network file system."
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  any
)
_http="https://github.com"
_ns="themartiancompany"
url="${_http}/${_ns}/${pkgname}"
license=(
  'AGPL3'
)
depends=(
  "evm-contracts-tools"
  "evm-wallet"
  "encoding-tools"
  "libcrash-bash"
  "libcrash-js"
)
_os="$( \
  uname \
    -o)"
[[ "${_os}" != "GNU/Linux" ]] && \
[[ "${_os}" == "Android" ]] && \
  depends+=(
  )
optdepends=(
)
[[ "${_os}" == 'Android' ]] && \
  optdepends+=(
  )
makedepends=(
  'make'
  'solidity-compiler'
)
if [[ "${_solc}" == "true" ]]; then
  makedepends+=(
    "solidity=0.8.24"
  )
elif [[ "${_hardhat}" == "true" ]]; then
  makedepends+=(
    "hardhat"
  )
fi
checkdepends=(
  "shellcheck"
)
source=()
sha256sums=()
_url="${url}"
_tag="${_commit}"
_tag_name="commit"
_tarname="${pkgname}-${_tag}"
[[ "${_offline}" == "true" ]] && \
  _url="file://${HOME}/${pkgname}"
[[ "${_git}" == true ]] && \
  makedepends+=(
    "git"
  ) && \
  source+=(
    "${_tarname}::git+${_url}#${_tag_name}=${_tag}?signed"
  ) && \
  sha256sums+=(
    SKIP
  )
[[ "${_git}" == false ]] && \
  if [[ "${_tag_name}" == 'pkgver' ]]; then
    _tar="${_tarname}.tar.gz::${_url}/archive/refs/tags/${_tag}.tar.gz"
    _sum="d4f4179c6e4ce1702c5fe6af132669e8ec4d0378428f69518f2926b969663a91"
  elif [[ "${_tag_name}" == "commit" ]]; then
    _tar="${_tarname}.zip::${_url}/archive/${_commit}.zip"
    _sum="d8ae1169f559927a5a15349c523fd5d6fc0376eaa7b89e8c1dad5eeee237a5f6"
  fi && \
    source+=(
      "${_tar}"
    ) && \
    sha256sums+=(
      "${_sum}"
    )
validpgpkeys=(
  # Truocolo <truocolo@aol.com>
  '97E989E6CF1D2C7F7A41FF9F95684DBE23D6A3E9'
  'DD6732B02E6C88E9E27E2E0D5FC6652B9D9A6C01'
)

check() {
  cd \
    "${_tarname}"
  make \
    -k \
    check
}

build() {
  cd \
    "${_tarname}"
  if [[ "${_solc}" == "true" ]]; then
    SOLIDITY_COMPILER_BACKEND="solc" \
    make \
      all
  fi
  if [[ "${_hardhat}" == "true" ]]; then
    SOLIDITY_COMPILER_BACKEND="hardhat" \
    make \
     all
  fi
}

package() {
  cd \
    "${_tarname}"
  make \
    DESTDIR="${pkgdir}" \
    PREFIX="/usr" \
    install
  if [[ "${_solc}" == "true" ]]; then
    make \
      DESTDIR="${pkgdir}" \
      PREFIX="/usr" \
      install-contracts-deployments-solc
  fi
  if [[ "${_hardhat}" == "true" ]]; then
    make \
      DESTDIR="${pkgdir}" \
      PREFIX="/usr" \
      install-contracts-deployments-hardhat
  fi
}

# vim: ft=sh syn=sh et
