---
title: Tips and Tricks
description: 
published: true
date: 2025-07-23T16:30:53.669Z
tags: tips, tricks
editor: markdown
dateCreated: 2024-04-05T10:25:57.151Z
---

# Tips and Tricks

## Arch Linux GPG Signature is not valid

If you are downloading a new application or upgrading a system and you face the problem that indicates the GPG Signature is not valid, you should to this things:

### Update the archlinux-keyring package

if the problem with gpg is comming from archlinux packages, you need to reinstall this package to get latest keys.

```bash
sudo pacman -Sy
sudo pacman -S archlinux-keyring
```

## Parch Linux GPG Signature is not valid

If you're experiencing issues with GPG signatures in Parch Linux, follow these steps to temporarily disable signature verification, install the updated keyring, and then restore normal behavior.

1. Temporarily disable GPG signature checks for PPR and PCP repositories

Edit the /etc/pacman.conf file and locate the [ppr] and [pcp] sections. Change their SigLevel to Never:
```
[ppr]
SigLevel = Never
Include = /etc/pacman.d/parch-mirrors

[pcp]
SigLevel = Never
Include = /etc/pacman.d/parch-mirrors
```
2. Update the keyring package

Now, install the latest parchlinux-keyring package:
```
sudo pacman -Sy parchlinux-keyring
```
This will install the trusted GPG keys required to validate Parch Linux packages.

3. Restore the original SigLevel settings

Once the keyring is installed, revert the SigLevel settings for [ppr] and [pcp] back to:

```
[ppr]
SigLevel = Optional TrustAll
Include = /etc/pacman.d/parch-mirrors

[pcp]
SigLevel = Optional TrustAll
Include = /etc/pacman.d/parch-mirrors
```

## Live system root space size is low

If you need to use Parch Linux live and you need more space for the live root, you need to run this command:

```bash
sudo mount -o remount,size=1G /run/archiso/cowspace
```

The command Above would increase the root file system to 1G , if you need more space change the 1G in command to something else for example: 4G

