---
title: KDE Plasma
description: 
published: true
date: 2024-10-17T10:15:38.437Z
tags: parchlinux, plasma, kde
editor: markdown
dateCreated: 2024-10-17T10:15:35.044Z
---

# KDE Plasma


## Was ist kde plasma?

KDE Plasma ist eine funktionsreiche und hochgradig anpassbare Desktopumgebung, die ein modernes und intuitives Benutzererlebnis bietet. Es ist bekannt für seine Flexibilität, umfangreichen Anpassungsoptionen und eine breite Palette an Anwendungen und Tools.

Parch Linux Plasma ist die **Flaggschiff** Version von Parch Linux.

![screenshot](https://raw.githubusercontent.com/parchlinux/parch-iso-plasma/main/image/screenshot.png)


## Installation

Sie können Plasma installieren, indem Sie Parch Linux Plasma installieren oder Ihren Desktop ändern.

Um den Desktop zu ändern, müssen Sie diese Pakete installieren:

```bash
sudo pacman -S plasma konsole kate dolphin sddm ark # for minimal installation

sudo pacman -S plasma konsole kate dolphin sddm ark plasmatube tokodon merkuro neochat marknote # for full ParchLinux plasma packages

```
> 
> Wenn Sie von der neuesten Version von Gnome migrieren, denken Sie daran, `QT_QPA_PLATFORMTHEME=qt6ct` aus `/etc/envierment`
{.is-info}


## Tips and Tricks

### Einen regionalen Screenshot erstellen

Durch Drücken von <kbd>Meta</kbd> + <kbd>Umschalt</kbd> + <kbd>Druck</kbd> können Sie mit Spectacle einen Bildschirmbereich auswählen, um einen Screenshot zu erstellen.

### Ändern des Menüsymbols zum ParchLinux-Logo

Derzeit wenden wir das Parchlogo nicht standardmäßig auf das Anwendungsmenü an. Um es zu ändern, klicken Sie mit der rechten Maustaste auf das Menü und dann auf `Anwendungsmenü konfigurieren`. Wählen Sie dann parch-logo.svg von diesem Speicherort aus:
`/usr/share/pixmaps/parch-logo.svg`

### Firefox KDE-Dateiauswahl

Damit Firefox besser mit KDE zusammenarbeitet, können Sie entweder das Paket `firefox-kde-opensuse`^AUR^ installieren oder die Einstellung manuell ändern:


Um den KDE-Dateiwähler in Firefox 64 oder neuer zu verwenden, installieren Sie `xdg-desktop-portal` und `xdg-desktop-portal-kde` und setzen Sie dann `widget.use-xdg-desktop-portal.file-picker` in `about:config` auf 1.