# my-aur

## Packages

| package                   | description                                                                  |
|---------------------------|------------------------------------------------------------------------------|
| crow-git                  | Crow is very fast and easy to use `C++` micro web frame                      |
| hotspot-appimage          | The linux perf GUI for performance analysis                                  |
| ocaml-easy-format         | Pretty-printing library for `OCaml`                                          |
| ocaml-ocp-indent          | Indentation tool for `OCaml`, to be used from editors like `Emacs` and `Vim` |
| ocaml-yojson              | Low level JSON library for `OCaml`                                           |
| ocaml-biniou              | An optimized parsing and print library for `OCaml`                           |
| ocaml-ppx_yojson_conv_lib | Runtime lib for ppx_yojson_conv                                              |
| merlin                    | Context sensitive completion for `OCaml` in `Vim` and `Emacs`                |

__merlin__ requires the version of
[dune](https://www.archlinux.org/packages/community/x86_64/dune/) larger than **1.8.0**.

Using the following PKGBUILD to upgrade to **2.2.0**.

``` shell
pkgname=dune
pkgver=2.2.0
pkgrel=1
pkgdesc="A composable build system for OCaml (formerly jbuilder)"
arch=(x86_64)
url="https://github.com/ocaml/dune"
license=(Apache)
depends=(glibc ocaml ocaml-findlib)
provides=(jbuilder)
conflicts=(jbuilder)
replaces=(jbuilder)
source=("${url}/releases/download/${pkgver}/${pkgname}-${pkgver}.tbz")
sha256sums=('ab5eb970c21641a6f3034448218cdc1c138512b906c7d2f67fea41ecd98d8bf4')

build() {
    cd ${pkgname}-${pkgver}
    make release
}

package() {
    cd ${pkgname}-${pkgver}

    make DESTDIR="${pkgdir}" INSTALL_ARGS="--prefix=/usr --libdir='lib/ocaml'" install

    # Fix doc and man install
    rm -r "${pkgdir}"/usr/doc
    install -dm755 "${pkgdir}"/usr/share
    mv "${pkgdir}"/usr/{man,share/}
}
```
