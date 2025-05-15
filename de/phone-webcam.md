---
title: Die Nutzung Ihres Android-Telefons als Webcam
description: 
published: true
date: 2025-05-15T11:32:21.302Z
tags: parch, parchlinux, scrcpy, webcam
editor: markdown
dateCreated: 2025-05-15T11:32:21.302Z
---

# Wie verwendet man ein Android-Telefon als Webcam in Parch Linux?


## Abhängigkeiten installieren

Zuerst musst du einige Abhängigkeiten installieren:

```bash
sudo pacman -S scrcpy dkms base-devel linux-headers v4l2loopback-dkms
```

Dann müssen Sie das Modul laden:

```bash
sudo modprobe v4l2loopback exclusive_caps=1
```

## Verwendung

### Kamerafreigabe

Um die Frontkamera zu verwenden, aktiviere zuerst **USB-Debugging** auf deinem Telefon, verbinde dein Telefon dann per Kabel und führe diesen Befehl im Terminal aus:

```bash
scrcpy --video-source=camera --camera-size=1920x1080 --camera-facing=front --v4l2-sink=/dev/video0 --no-playback --no-window
```

Für die hintere Kamera ändere einfach ```--camera-facing=front``` zu ```--camera-facing=back``` .

#### Kamera testen

Einfach OBS öffnen oder diesen Befehl ausführen:

```bash
ffplay /dev/video0
```

### Mikrofonfreigabe

Für das Mikrofon können Sie diesen Befehl ausführen:

```bash
scrcpy --no-video --audio-source=mic --no-window
```

Das würde dein Telefonmikrofon als Systemaudio freigeben.

