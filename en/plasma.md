---
title: KDE Plasma
description: 
published: true
date: 2024-10-17T09:39:53.561Z
tags: parchlinux, plasma, kde
editor: markdown
dateCreated: 2024-05-28T14:19:07.604Z
---

# KDE Plasma


## What is kde plasma?

KDE Plasma is a feature-rich and highly customizable desktop environment that offers a modern and intuitive user experience. It is known for its flexibility, extensive customization options, and a wide range of applications and tools.

Parch Linux Plasma is the **Flagship** version of Parch Linux.


![screenshot](https://raw.githubusercontent.com/parchlinux/parch-iso-plasma/main/image/screenshot.png)


## Installation

You can install Plasma by installing Parch Linux Plasma or changing your desktop.

For changing Desktop you need to install this packages:

```bash
sudo pacman -S plasma konsole kate dolphin sddm ark # for minimal installation

sudo pacman -S plasma konsole kate dolphin sddm ark plasmatube tokodon merkuro neochat marknote # for full ParchLinux plasma packages

```
> 
> If you are migrating from latest version of gnome, remmeber to remove `QT_QPA_PLATFORMTHEME=qt6ct` from `/etc/envierment`
{.is-info}


## Tips and Tricks

### Taking a Regional screenshot

By pressing <kbd>meta</kbd> + <kbd>shift</kbd> + <kbd>print</kbd> spectacle would let you select a region of screen to take screenshot.

### Changing menu icon to ParchLinux logo

For now we don't apply the parchlogo to the application menu by default. for changing it right click on the menu and click on `Configure application menu` then selec parch-logo.svg from this location:
`/usr/share/pixmaps/parch-logo.svg`

### Firefox KDE file choser

For making firefox to work better with kde, either you can install `firefox-kde-opensuse`^AUR^ package or change the setting manually:


To use the KDE file picker in Firefox 64 or newer, install `xdg-desktop-portal` and `xdg-desktop-portal-kde`, then set `widget.use-xdg-desktop-portal.file-picker` to 1 in `about:config`