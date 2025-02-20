---
title: Waydroid on Parch Linux
description: How to run android apps in Parch?
published: true
date: 2024-07-22T16:02:53.406Z
tags: parchlinux, android, waydroid, emulator
editor: markdown
dateCreated: 2024-07-22T15:57:03.046Z
---

# Waydroid
Waydroid is a container-based approach to boot a full Android system on a regular GNU/Linux system. 

## Installation

In Parch Linux there is a script called ```waydroid-helper```^PPR^ which can be used to install waydroid with a non-gapps image (an android image without google apps such as play store ) on Parch Linux.


For start you need to install the Script from Parch Packages Repository:

```bash
sudo pacman -S waydroid-helper
```

### Checking system requirements

To check whether if your system is compatible with waydroid, you need to run ```waydroid-checker``` script.

```bash
waydroid-checker
```

After running it you will be prompted with this screen:

![waydroid-checker1.png](/waydroid-checker1.png)

Click on **Start Test** to begin.

![waydroid-checker2.png](/waydroid-checker2.png)

After the test is finished, **if your CPU passed you can continue with the installation**


### Installing Waydroid

you can run the ```waydroid-installer``` script to begin the installation:

```bash
waydroid-installer
```

### Post Installation

After the installation is finished you should init waydroid:

```bash
sudo waydroid init
```

after its done, if you are on **wayland** you can run waydroid from your application menu.


## X11

For running waydroid under **X11** You need to run ```waydroid-x11``` from terminal:

```bash
waydroid-x11
```

It would launch waydroid in your x11 session like XFCE, Mate etc... under weston.
