---
title: Tips and Tricks
description: 
published: true
date: 2024-04-05T10:27:08.108Z
tags: tips, tricks
editor: markdown
dateCreated: 2024-04-05T10:25:57.151Z
---

# Tips and Tricks

## GPG Signature is not valid

If you are downloading a new application or upgrading a system and you face the problem that indicates the GPG Signature is not valid, you should to this things:

### Update the archlinux-keyring package

if the problem with gpg is comming from archlinux packages, you need to reinstall this package to get latest keys.

```bash
sudo pacman -Sy
sudo pacman -S archlinux-keyring
```


## Live system root space size is low

If you need to use Parch Linux live and you need more space for the live root, you need to run this command:

```bash
sudo mount -o remount,size=1G /run/archiso/cowspace
```

The command Above would increase the root file system to 1G , if you need more space change the 1G in command to something else for example: 4G

