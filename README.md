BroTracker Arch Linux Package (PKGBUILD)

This directory contains the PKGBUILD script to package the BroTracker desktop application for Arch Linux and Arch-based Linux distributions (e.g., Manjaro, EndeavourOS).

The package extracts and repackages the official .deb release to integrate cleanly into Arch Linux following Arch packaging guidelines.

📋 Prerequisites

Ensure you have the basic Arch Linux build utilities and package extraction tools installed:

sudo pacman -S --needed base-devel libarchive


The package declares necessary system dependencies (such as gtk3, nss, alsa-lib, systemd-libs, etc.), which pacman will handle automatically during installation.

🛠️ How to Build and Install

Clone or Download this directory containing the PKGBUILD file:

cd /path/to/directory-containing-pkgbuild


Build and Install the package using makepkg:

makepkg -si


Command Flags Breakdown:

-s (--syncdeps): Automatically downloads and installs any missing runtime/build dependencies via pacman.

-i (--install): Automatically installs the compiled package upon successful build.

📦 Manual Installation (Alternative)

If you ran makepkg -s without the -i flag, build output files will be created in your working directory. You can install the package file manually using:

sudo pacman -U brotracker-*.pkg.tar.zst


🚀 How to Run

Once installed, BroTracker can be launched in two ways:

Application Menu: Search for "BroTracker" in your desktop launcher (GNOME, KDE, XFCE, Rofi, etc.).

Terminal: Run the executable directly:

brotracker


🗑️ How to Uninstall

To remove BroTracker along with unused dependencies:

sudo pacman -Rs brotracker


🔄 Maintaining & Updating

To update the package when a new upstream version of BroTracker is released:

Edit PKGBUILD and update pkgver to the new version:

pkgver=X.Y.Z


Rebuild and update the package:

makepkg -Csi


(The -C flag cleans up old source and build directories before rebuilding.)
