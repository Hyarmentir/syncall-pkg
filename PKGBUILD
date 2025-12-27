# Maintainer: "Gustav Åkerström <gustavakerstrom@gmail.com>"
# Contributor: "Sergey Malkin <adresatt@gmail.com>"

pkgname=syncall-gtasks-tw
_gitname="syncall-gtasks-tw"
pkgver=r242.7d32371
pkgrel=1
pkgdesc="Bi-directional synchronization between services such as Taskwarrior, Google Calendar, Notion, Asana, and more"
url="https://github.com/Hyarmentir/syncall-gtasks-tw"
arch=("i686" "x86_64")
license=("MIT")
depends=(
  "python>=3.8" "python-yaml>=5.3.1" "python-bidict>=0.21.4" "python-click>=8.1.7"
  "python-loguru>=0.5.3" "python-dateutil>=2.9.0" "python-item_synchronizer>=1.1.5" 
  "python-bubop>=0.1.12" "python-setuptools>=72.1.0"
  "python-google-api-python-client"
  "python-google-auth-oauthlib"
  "python-taskw-ng=0.2.7"
  "python-xdg-base-dirs"
)
makedepends=(
  "python-installer" "python-poetry"
  )
optdepends=(
  "python-asana>=1.0.0" 
  "python-caldav>=0.11.0" 
  "python-icalendar>=5.0.13"
  "task>=2.6"
  "python-xattr>=0.99.9"
  "python-gkeepapi"
  "python-notion-client"
)

provides=("syncall")
conflicts=("syncall")

#source=("git+https://github.com/Hyarmentir/syncall-gtasks-tw")
source=("git+file:///home/antoinen/workspace/syncall-gtasks-tw")
sha256sums=('SKIP')

pkgver() {
  cd "$_gitname"
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short=7 HEAD)"
}

build() {
  cd "$srcdir/$_gitname"
  poetry install --extras "google tw"
  poetry build
}

package() {
  cd "$srcdir/$_gitname"
  python -m installer --destdir="$pkgdir" dist/*.whl
}
