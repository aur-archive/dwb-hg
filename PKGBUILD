# Contributor: portix <portix@gmx.net>

pkgname=dwb-hg
pkgver=1955
pkgrel=1
pkgdesc="A webkit web browser with vi-like keyboard shortcuts, latest hg-pull" 
url="http://portix.bitbucket.org/dwb/"
arch=('i686' 'x86_64')
license=('GPL')
depends=('webkitgtk2' 'desktop-file-utils')
provides=(dwb)
install=dwb.install
conflicts=('dwb' 'dwb-gtk3-hg' 'dwb-gtk3')
makedepends=('mercurial' 'json-c')

_hgroot="https://bitbucket.org/portix"
_hgrepo="dwb"

build() {
  cd "$srcdir"
  msg "Connecting to Mercurial server...."

  if [[ -d "$_hgrepo" ]]; then
    cd "$_hgrepo"
    hg pull -u
    msg "The local files are updated."
  else
    hg clone "$_hgroot/$_hgrepo"
  fi

  msg "Mercurial checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_hgrepo-build"
  cp -r "$srcdir/$_hgrepo" "$srcdir/$_hgrepo-build"
  cd "$srcdir/$_hgrepo-build"

  make 
}
package() {
  cd "${srcdir}/${_hgrepo}-build"
  make DESTDIR="${pkgdir}" install \
      BASHCOMPLETION=/usr/share/bash-completion/completions
}
