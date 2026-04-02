# Maintainer: ZhongHongSoftware — Zeta <3380089537@qq.com>
pkgname=mengxios-dotfile
pkgver=1.6.0
pkgrel=1
pkgdesc="Mengxio's personal dotfiles for hyprland, with full dependency injection"
arch=('any')
depends=('hyprland' 'kitty' 'dolphin' 'firefox' 'neovim' 'libnotify' 'fastfetch' 'sddm' 'polkit-kde-agent' 'wqy-zenhei' 'qt6-wayland' 'qt6-declarative' 'libxcb' 'xcb-util-cursor' 'python-gobject' 'python-cairo' 'dms-shell')
source=("dotfiles.zip" "mengxios-dotfile-session" "mengxios-dotfile.desktop" "sddm.conf")
sha256sums=('SKIP' 'SKIP' 'SKIP' 'SKIP')
package() {
  install -dm755 "$pkgdir/usr/share/$pkgname"
  unzip -q dotfiles.zip -d "$srcdir"
  cp -r "$srcdir/dotfiles"/. "$pkgdir/usr/share/$pkgname/"
  install -Dm755 "$srcdir/mengxios-dotfile-session" "$pkgdir/usr/bin/mengxios-dotfile-session"
  install -Dm644 "$srcdir/mengxios-dotfile.desktop" "$pkgdir/usr/share/wayland-sessions/mengxios-dotfile.desktop"
  install -Dm644 "$srcdir/sddm.conf" "$pkgdir/etc/sddm.conf"
}
