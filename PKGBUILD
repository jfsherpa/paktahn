# Contributor: Leslie P. Polzer <polzer@gnu.org>
# Maintainer: Brit Butler <redline6561@gmail.com>

pkgname=paktahn
pkgver=0.9.6.0
libver=0.9.3
pkgrel=1
pkgdesc="The kick-ass package manager for Arch Linux!"
arch=('i686' 'x86_64')
depends=('pacman' 'readline' 'sudo' 'svn')
makedepends=('sbcl>=1.0.32')
license=('GPL')
url="http://github.com/skypher/paktahn"
options=(!strip)
install="paktahn.install"
source=("http://redlinernotes.com/docs/paktahn-makedeps-$libver.tbz2"
        "http://redlinernotes.com/docs/paktahn-${pkgver}.tar.bz2")

build() {
  cd "$srcdir"

  # compile
  SBCL=sbcl

  $SBCL \
       --noinform --lose-on-corruption --end-runtime-options \
       --no-userinit --no-sysinit \
       --eval "(pushnew :paktahn-deploy *features*)" \
       --eval "(require :asdf)" \
       --eval "(setf asdf:*central-registry*
                    '(\"$srcdir/\" \"$srcdir/clbuild.paktahn/systems/\"))" \
       --eval "(asdf:oos 'asdf:load-op 'paktahn)" \
       --eval "(pak::build-core :forkp nil)"

  # install binary
  mkdir -p $pkgdir/usr/bin
  install -m755 paktahn $pkgdir/usr/bin

  # install helper scripts
  mkdir -p $pkgdir/usr/lib/paktahn
  for helper in pkgbuild-helper.sh makepkg-helper.sh; do
    install -m755 "$helper" $pkgdir/usr/lib/paktahn
  done

  # create convenience symlink
  cd $pkgdir/usr/bin
  ln -s paktahn pak
}

md5sums=('aa71c5e639e86bee3afe7d4e27653649'
         '2afeedbbf3da14bc1fbd45f91e0d4a66')
sha1sums=('1fb3e04732d00c68e7b8aa7ae0a18e9f98359e5f'
          'cc5941cc93b483f331d346151b5aa0f69c2c59f7')
