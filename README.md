# BroTracker Arch Linux Package (`PKGBUILD`)

This directory contains the `PKGBUILD` script to package the **BroTracker** desktop application for Arch Linux and Arch-based Linux distributions (e.g., Manjaro, EndeavourOS).

The package extracts and repackages the official `.deb` release to integrate cleanly into Arch Linux following Arch packaging guidelines.

---

## 📋 Prerequisites

Ensure you have the basic Arch Linux build utilities and package extraction tools installed:

```bash
sudo pacman -S --needed base-devel libarchive
```

The package declares necessary system dependencies (such as `gtk3`, `nss`, `alsa-lib`, `systemd-libs`, etc.), which `pacman` will handle automatically during installation.

---

## 🛠️ How to Build and Install

1. **Clone or Download** this directory containing the `PKGBUILD` file:
   ```bash
   cd /path/to/directory-containing-pkgbuild
   ```

2. **Build and Install** the package using `makepkg`:
   ```bash
   makepkg -si
   ```

### Command Flags Breakdown:
* **`-s` (`--syncdeps`)**: Automatically downloads and installs any missing runtime/build dependencies via `pacman`.
* **`-i` (`--install`)**: Automatically installs the compiled package upon successful build.

---

## 📦 Manual Installation (Alternative)

If you ran `makepkg -s` without the `-i` flag, build output files will be created in your working directory. You can install the package file manually using:

```bash
sudo pacman -U brotracker-*.pkg.tar.zst
```

---

## 🚀 How to Run

Once installed, BroTracker can be launched in two ways:

1. **Application Menu**: Search for "BroTracker" in your desktop launcher (GNOME, KDE, XFCE, Rofi, etc.).
2. **Terminal**: Run the executable directly:
   ```bash
   brotracker
   ```

---

## 🗑️ How to Uninstall

To remove BroTracker along with unused dependencies:

```bash
sudo pacman -Rs brotracker
```

---

## 🔄 Maintaining & Updating

To update the package when a new upstream version of BroTracker is released:

1. Edit `PKGBUILD` and update `pkgver` to the new version:
   ```bash
   pkgver=X.Y.Z
   ```
2. Rebuild and update the package:
   ```bash
   makepkg -Csi
   ```
   *(The `-C` flag cleans up old source and build directories before rebuilding.)*
