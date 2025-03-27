---
title: Virtualisierung auf Parch Linux
description: Die Virtualisierung erstellt eine virtuelle Maschine, die ein Betriebssystem enthält, das in Ihrem Hauptsystem funktioniert.
published: true
date: 2025-03-27T13:07:20.259Z
tags: parch, virtual, virtualization
editor: markdown
dateCreated: 2025-03-27T12:44:00.864Z
---

# Was ist Virtualisierung?

Aus [Wikipedia](https://de.wikipedia.org/wiki/Virtualisierung_(Informatik)):

> In der Informatik ist die Virtualisierung die Handlung, eine virtuelle Version von etwas auf demselben Abstraktionsniveau zu schaffen, einschließlich virtueller [Rechenhardware](https://de.wikipedia.org/wiki/Hardware), [Speichergeräte](https://de.wikipedia.org/wiki/Datenspeicher) und [Netzwerkressourcen](https://de.wikipedia.org/wiki/Rechnernetz).

Eine virtuelle Maschine ist eine simulierte Computer, die innerhalb eines anderen Computers läuft. Die simulierte Computer wird oft Gast genannt, während die reale Maschine Host genannt wird.

Beispiele für virtuelle Client-Software umfassen [Oracle VirtualBox](https://www.virtualbox.org), [GNOME Boxes](https://help.gnome.org/users/gnome-boxes/stable/), [VMware Workstation](https://www.vmware.com/products/workstation-player.html) (Nicht FOSS) und [QEMU](https://www.qemu.org).

Obwohl du frei bist, welche Client-Software du verwenden möchtest zu wählen, empfehlen wir dir [GNOME Boxes](https://help.gnome.org/users/gnome-boxes/stable) zu verwenden.

## GNOME Boxes

> Boxes ist eine Anwendung, die Ihnen Zugang zu virtuellen Maschinen gewährleistet, die lokal oder entfernt betrieben werden. Die Anwendung ermöglicht es Ihnen auch, sich mit dem Bildschirm eines entfernten Computers zu verbinden.

### Installieren Boxes

Das Installieren von Boxen auf Parch ist wie Alphabet einfach. Alles, was Sie tun müssen, ist, `sudo pacman -S gnome-boxes` in Ihrem Terminal auszuführen und anschließend neu zu starten. Boxes werden nach dem Booten ihres Computers sichtbar sein.

## Oracle VirtualBox

> VirtualBox ist ein leistungsfähiges x86- und AMD64/Intel64-Virtualisierungsprodukt für Unternehmen sowie den privaten Gebrauch. Nicht nur ist VirtualBox ein extrem üppig ausgestattetes, hoch leistungsfähiges Produkt für Unternehmenskunden, es ist auch die einzige professionelle Lösung, die als quelloffene Software unter den Bedingungen der GNU General Public License (GPL) Version 3 frei verfügbar ist.


### Installieren VirtualBox

Sie können das Kernpaket von VirtualBox installieren, indem Sie `sudo pacman -S virtualbox` ausführen.

Als nächstes solltest du `sudo pacman -S virtualbox-host-dkms` ausführen.

Um die von [virtualbox-host-dkms](https://archlinux.org/packages/?name=virtualbox-host-dkms) bereitgestellten VirtualBox-Module zu kompilieren, benötigen Sie außerdem die passenden Header-Pakete für Ihren installierten Kernel, z. B.:

`sudo pacman -S linux-header` für Linux kernel
`sudo pacman -S linux-lts-headers` für Linux-LTS kernel
`sudo pacman -S linux-zen-headers` für Linux-ZEN kernel
`sudo pacman -S linux-hardened-headers` für Linux-HARDENED kernel

Vergessen Sie nicht, nach der Installation neu zu starten.

### Aktivieren Sie zusätzliche Funktionen von VirtualBox

> Das Oracle VirtualBox Extension Pack enthält [zusätzliche Funktionen](https://www.virtualbox.org/manual/ch01.html#intro-installing) und wird lediglich für den persönlichen Einsatz unter einer nicht freien Lizenz veröffentlicht. Um es zu installieren, steht das Paket [virtualbox-ext-oracle](https://aur.archlinux.org/packages/virtualbox-ext-oracle/)AUR zur Verfügung.

Aus irgendwelchen Gründen sind zusätzliche Funktionen in VirtualBox (z. B. das Mounten eines externen Medien Geräts wie einer USB-Stick im Gast) nicht im Kernpaket enthalten, und Sie müssen das Erweiterungspaket installieren, um diese Funktionen zu nutzen.

Sie können dieses Paket installieren und diese Funktionen verwenden nach:

1. Führen Sie den Befehl `paru -S virtualbox-ext-oracle --noconfirm` im Terminal aus. (`Paru` ist standardmäßig in Parch Linux enthalten, aber Sie können stattdessen `yay` oder `aura` verwenden.)

2. Führen Sie den Befehl `sudo usermod -aG vboxusers YOUR-USERNAME` im Terminal aus. (Ersetzen Sie `YOUR-USERNAME` im Befehl durch Ihren Benutzernamen.)

Vergessen Sie am Ende nicht zum Neustart, da dies notwendig ist.