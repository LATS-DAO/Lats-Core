
Debian
====================
This directory contains files used to package latsd/lats-qt
for Debian-based Linux systems. If you compile latsd/lats-qt yourself, there are some useful files here.

## lats: URI support ##


lats-qt.desktop  (Gnome / Open Desktop)
To install:

	sudo desktop-file-install lats-qt.desktop
	sudo update-desktop-database

If you build yourself, you will either need to modify the paths in
the .desktop file or copy or symlink your lats-qt binary to `/usr/bin`
and the `../../share/pixmaps/lats128.png` to `/usr/share/pixmaps`

lats-qt.protocol (KDE)

