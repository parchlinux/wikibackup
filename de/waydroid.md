---
title: Waydroid auf Parch Linux
description: Wie führe ich Android-Apps in Parch aus?
published: true
date: 2025-03-28T12:45:02.126Z
tags: parchlinux, android, waydroid, emulator
editor: markdown
dateCreated: 2025-03-28T12:45:02.126Z
---

# Waydroid

Waydroid ist eine containerbasierte Methode, um ein volles Android-System auf einem regulären GNU/Linux-System zu booten.

## Installation

In Parch Linux gibt es ein Skript namens ``waydroid-helper``^PPR^, das verwendet werden kann, um Waydroid mit einem non-GApps-Bild (einem Android-Bild ohne Google-Apps wie den Play Store) auf Parch Linux zu installieren.

Für Start müssen Sie das Skript von Parch Pakete Repository installieren:

```bash
sudo pacman -S waydroid-helper
```

### Systemanforderungen überprüfen

Prüfen Sie, ob Ihr System mit Waydroid kompatibel ist, müssen Sie das Skript `waydroid-checker` ausführen.

```bash
waydroid-checker
```

Nach dem Ausführen werden Sie mit diesem Bildschirm aufgefordert:

![waydroid-checker1.png](/waydroid-checker1.png)

Klicken Sie auf **Start Test**, um zu beginnen.

![waydroid-checker2.png](/waydroid-checker2.png)

Nach Abschluss des Tests **Wenn Ihre CPU bestanden hat, können Sie die Installation fortsetzen**

### Installieren von Waydroid

Sie können das Skript `Waydroid-Installer` ausführen, um die Installation zu beginnen:

```bash
waydroid-installer
```

### Post-Installation

Nach Abschluss der Installation sollten Sie Waydroid initieren:

```bash
sudo waydroid init
```

Nach Abschluss des Vorgangs, wenn du unter Wayland arbeitest, kannst du **Waydroid** über deinen Anwendungsverzeichnis starten.

## X11

Für die Ausführung von **waydroid unter X11** müssen Sie ```waydroid-x11``` von der Konsole ausführen:

```bash
waydroid-x11
```

Es würde WayDroid in Ihrer X11-Sitzung wie XFCE, MATE usw. unter Weston starten.