# Maintainer: Your Name <your.email@example.com>
pkgname=syncall
_pkgname=syncall
pkgver=1.8.8 # Replace with the actual version you want to package
pkgrel=1
pkgdesc="Versatile bi-directional synchronization tool"
arch=('any')
url="https://github.com/bergercookie/syncall"
license=('MIT')
depends=('python311')
makedepends=('git')
source=("https://github.com/bergercookie/$pkgname/archive/refs/tags/v$pkgver.tar.gz")
sha256sums=('dde09bd575b7fa5827b5bc2bff380db674490a000f41e51e860b6ec8f14ce6d6')

#prepare() {
#  cd "$srcdir/$pkgname-$pkgver"#

  # If you need to patch pyproject.toml for the xdg-base-dirs issue,
  # or any other files, you would do it here.
  # For example:
  #sed -i 's/from xdg/from xdg_base_dirs/g' syncall/taskwarrior/taskwarrior_side.py
  #sed -i 's/xdg/xdg-base-dirs/g' pyproject.toml"
#

build() {
  cd "$srcdir/$pkgname-$pkgver"

  # Create a virtual environment using python3.11
  python3.11 -m venv venv

  # Activate the venv and install pip and poetry and then the project dependencies
  source venv/bin/activate
  python3.11 -m ensurepip --upgrade 
  pip install poetry
  poetry install --all-extras
}

package() {
  cd "$srcdir/$pkgname-$pkgver"

  # Copy the application code and the virtual environment to the package directory
  install -d "${pkgdir}/usr/share/${pkgname}"
  cp -r . "${pkgdir}/usr/share/${pkgname}/"

  # Create wrapper scripts for the executables in /usr/bin
  install -d "${pkgdir}/usr/bin"
  # Extract script names from pyproject.toml's [tool.poetry.scripts] section
  scripts=$(awk '/^\[tool\.poetry\.scripts\]/{f=1;next} /^\[/{f=0} f&&/ = /{print $1}' pyproject.toml)
  for script in $scripts; do
    # Create a wrapper that executes the sync script with the venv's python
    echo "#!/bin/sh" > "${pkgdir}/usr/bin/${script}"
    echo "exec /usr/share/${pkgname}/venv/bin/python -m syncall.scripts.${script} \"\$@\"" >> "${pkgdir}/usr/bin/${script}"
    chmod +x "${pkgdir}/usr/bin/${script}"
  done
}
