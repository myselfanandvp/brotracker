# Maintainer: Your Name <you@example.com>
pkgname=brotracker
pkgver=0.1.12
pkgrel=1
pkgdesc="BroTracker desktop app"
arch=('x86_64')
url="https://brotracker.com"
license=('custom')
depends=(
  'alsa-lib'
  'atk'
  'cairo'
  'dbus'
  'expat'
  'fontconfig'
  'freetype2'
  'gdk-pixbuf2'
  'glib2'
  'gtk3'
  'libgl'
  'libnotify'
  'libpipewire'
  'libpulse'
  'libsecret'
  'libx11'
  'libxcomposite'
  'libxdamage'
  'libxext'
  'libxfixes'
  'libxi'
  'libxrandr'
  'libxrender'
  'libxtst'
  'mesa'
  'nspr'
  'nss'
  'pango'
  'systemd-libs'
  'vulkan-icd-loader'
  'xdg-utils'
)
makedepends=('libarchive')
source=("https://brotracker-prod.blr1.digitaloceanspaces.com/portal/brotracker-portal_${pkgver}_amd64.deb")
sha256sums=('SKIP')

package() {
  msg2 "Extracting data archive from .deb..."
  local data_archive
  data_archive=$(bsdtar -tf "brotracker-portal_${pkgver}_amd64.deb" | grep '^data\.tar\.')
  bsdtar -O -xf "brotracker-portal_${pkgver}_amd64.deb" "$data_archive" | bsdtar -C "$pkgdir" -xf -

  msg2 "Creating bin directory and symlink..."
  install -d "$pkgdir/usr/bin"

  # Find the main Electron executable deterministically
  local binary_path
  binary_path=$(find "$pkgdir/opt" -type f -executable \
    ! -name '*.so*' \
    ! -name 'chrome-sandbox' \
    ! -name 'chrome_crashpad_handler' \
    -printf '%s\t%p\n' | sort -rn | head -n 1 | cut -f2-)

  if [ -z "$binary_path" ]; then
    error "Could not find the main executable under opt/"
    return 1
  fi

  local rel_path="${binary_path#$pkgdir/}"
  ln -s "/$rel_path" "$pkgdir/usr/bin/brotracker"

  msg2 "Patching desktop entries..."
  for f in "$pkgdir/usr/share/applications/"*.desktop; do
    [ -f "$f" ] || continue
    sed -i -E 's#^Exec=("[^"]*"|[^ ]+)#Exec=brotracker#' "$f"
    # Ensure Icon field maps correctly to installed icon name
    sed -i -E 's#^Icon=.*#Icon=brotracker#' "$f"
  done
}
