---
title: Virtualization on Parch Linux
description: Virtualization is creating a virtual machine, containing an OS that works within your main system.
published: true
date: 2024-05-21T21:15:23.646Z
tags: 
editor: markdown
dateCreated: 2024-05-21T18:48:02.541Z
---


## What is **virtualization?**

From [Wikipedia](https://en.wikipedia.org/wiki/Virtualization):

> In computing, **virtualization** is the act of creating a virtual (rather than actual) version of something at the same abstraction level, including virtual [computer hardware](https://en.wikipedia.org/wiki/Computer_hardware) platforms, [storage devices](https://en.wikipedia.org/wiki/Data_storage_device), and [computer network](https://en.wikipedia.org/wiki/Computer_network) resources.

A virtual machine is a simulated computer running inside another computer. The simulated computer is often called guest, while the real machine is called host.

Popular examples of virtualization client softwares includes [Oracle VirtualBox](https://www.virtualbox.org/), [GNOME Boxes](https://help.gnome.org/users/gnome-boxes/stable/), [VMware Workstation](https://www.vmware.com/products/workstation-player.html) _(Not FOSS)_ and [QEMU](https://www.qemu.org/).

_While you're free to choose what client software you want to use,**we recommend you to use**_[ _**GNOME Boxes**_](https://help.gnome.org/users/gnome-boxes/stable/) _._

## GNOME Boxes

> Boxes is an application that gives you access to virtual machines, running locally or remotely. It also allows you to connect to the display of a remote computer.

### Installing Boxes

Installing Boxes on Parch is easy as alphabet. All you have to do is to run `sudo pacman -S gnome-boxes` in your terminal and reboot afterwards. You'll see Boxes after your computer boots up.

## Oracle VirtualBox

> VirtualBox is a powerful x86 and AMD64/Intel64 [virtualization](https://www.virtualbox.org/wiki/Virtualization) product for enterprise as well as home use. Not only is VirtualBox an extremely feature rich, high performance product for enterprise customers, it is also the only professional solution that is freely available as Open Source Software under the terms of the [GNU General Public License (GPL) version 3](https://www.virtualbox.org/wiki/GPLv3).

### Installing VirtualBox

You can install the core package of VirtualBox by running `sudo pacman -S virtualbox`.

Next, you should run `sudo pacman -S virtualbox-host-dkms`.

To compile the VirtualBox modules provided by [virtualbox-host-dkms](https://archlinux.org/packages/?name=virtualbox-host-dkms), you'll also need to to install the appropriate headers packages for your installed kernel, for example:

  * `sudo pacman -S linux-headers` for [Linux](https://archlinux.org/packages/?name=linux) kernel
  * `sudo pacman -S linux-lts-headers` for Linux-LTS kernel
  * `sudo pacman -S linux-zen-headers` for Linux-ZEN kernel
  * `sudo pacman -S linux-hardened-headers` for Linux-HARDENED kernel



Don't forget to reboot after installing.

### Enabling additional features of VirtualBox

> The _Oracle VirtualBox Extension Pack_ provides [additional features](https://www.virtualbox.org/manual/ch01.html#intro-installing) and is released under a non-free license **only available for personal use**. To install it, the [virtualbox-ext-oracle](https://aur.archlinux.org/packages/virtualbox-ext-oracle/)AUR package is available.

For some reasons, additional features on VirtualBox _(e.g. mounting an external media device like an USB stick to the guest)_ are not included in the core package and you need to install the extension pack to use these features.

You can install this package and use these features by:

  1. Running `paru -S virtualbox-ext-oracle --noconfirm` on your terminal. (`_paru_` __ comes included by default in Parch Linux, but you may want to use `_yay_` __ or `_aura_` __ instead.)
  2. Running `sudo usermod -aG vboxusers _YOUR-USERNAME_` __ on your terminal. (Put your username instead of `_YOUR-USERNAME_` __ in the command.)



At the end, don't forget to reboot, since it is necessary.

