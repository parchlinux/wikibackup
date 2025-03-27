---
title: Virtualisierung auf Parch Linux
description: Die Virtualisierung erstellt eine virtuelle Maschine, die ein Betriebssystem enthält, das in Ihrem Hauptsystem funktioniert.
published: true
date: 2025-03-27T12:44:00.864Z
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

### Installation Boxes

Das Installieren von Boxen auf Parch ist wie Alphabet einfach. Alles, was Sie tun müssen, ist, `sudo pacman -S gnome-boxes` in Ihrem Terminal auszuführen und anschließend neu zu starten. Boxes werden nach dem Booten ihres Computers sichtbar sein.

## Oracle VirtualBox

> VirtualBox ist ein leistungsfähiges x86- und AMD64/Intel64-Virtualisierungsprodukt für Unternehmen sowie den privaten Gebrauch. Nicht nur ist VirtualBox ein extrem üppig ausgestattetes, hoch leistungsfähiges Produkt für Unternehmenskunden, es ist auch die einzige professionelle Lösung, die als quelloffene Software unter den Bedingungen der GNU General Public License (GPL) Version 3 frei verfügbar ist.


### Installing VirtualBox

You can install the core package of VirtualBox by running sudo pacman -S virtualbox.

Next, you should run sudo pacman -S virtualbox-host-dkms. 

To compile the VirtualBox modules provided by virtualbox-host-dkms, you'll also need to to install the appropriate headers packages for your installed kernel, for example:

sudo pacman -S linux-headers for Linux kernel
sudo pacman -S linux-lts-headers for Linux-LTS kernel
sudo pacman -S linux-zen-headers for Linux-ZEN kernel
sudo pacman -S linux-hardened-headers for Linux-HARDENED kernel

Don't forget to reboot after installing.

Enabling additional features of VirtualBox

The Oracle VirtualBox Extension Pack provides additional features and is released under a non-free license only available for personal use. To install it, the virtualbox-ext-oracleAUR package is available.

For some reasons, additional features on VirtualBox (e.g. mounting an external media device like an USB stick to the guest) are not included in the core package and you need to install the extension pack to use these features.

You can install this package and use these features by: 

Running paru -S virtualbox-ext-oracle --noconfirm on your terminal. (paru comes included by default in Parch Linux, but you may want to use yay or aura instead.)
Running sudo usermod -aG vboxusers YOUR-USERNAME on your terminal. (Put your username instead of YOUR-USERNAME in the command.)

At the end, don't forget to reboot, since it is necessary.