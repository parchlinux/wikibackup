---
title: Debian Chroot in Parch Linux
description: A Guide to have debian under Parch Linux
published: true
date: 2024-04-05T10:42:59.452Z
tags: debian, parch
editor: markdown
dateCreated: 2024-04-05T10:37:55.039Z
---

# What is a Chroot?
The chroot Linux utility can modify the working root directory for a process, limiting access to the rest of the file system.


## how to have a Debian chroot inside ParchLinux?

1. Install Debootstrap

```bash
sudo pacman -Sy
sudo pacman -S debootstrap
```

2. Make a Folder inside /opt for your debian new root

```bash
sudo mkdir /opt/debian
```

3. Set Debootstrap location and start Debootstraping :D

```bash
DEBOOTSTRAP_DIR=/opt/debootstrap/usr/share/debootstrap /opt/debootstrap/usr/sbin/debootstrap --arch amd64 bookworm /opt/debian/ http://ftp.uk.debian.org/debian/
```

- **Note** : You can change the debian version by changing the bookworm to your version codename. You can find debian codenames [here](https://wiki.debian.org/DebianReleases#Production_Releases).

4. Mount the Directories

```bash
mount -t proc proc /opt/debian/proc/
mount -t sysfs sys /opt/debian/sys/
mount -o bind /dev /opt/debian/dev/
mount -o bind /dev/pts /opt/debian/dev/pts/
```

5. Setup the repositories for your chrooted system

```bash
cat > /opt/debian/etc/apt/sources.list << 'EOF'
deb http://ftp.uk.debian.org/debian/ bookworm main non-free contrib
deb-src http://ftp.uk.debian.org/debian/ bookworm main non-free contrib

deb http://security.debian.org/ bookworm/updates main non-free contrib
deb-src http://security.debian.org/ bookworm/updates main non-free contrib

deb http://ftp.uk.debian.org/debian/ bookworm-updates main non-free contrib
deb-src http://ftp.uk.debian.org/debian/ bookworm-updates main non-free contrib
EOF
```

- **Note** : Change the Codename to your installed Version

6. Chroot to your debian

```bash
chroot /opt/debian /bin/bash
```

7. Upgrade the Debian and regenerate the locales:

```bash
apt-get update && apt-get dist-upgrade
apt-get install locales
dpkg-reconfigure locales
```

8. Add a name to /etc/hosts

```bash
echo mywonderfulldebian >> /etc/hosts
```

## Optional

1. Add a new user to the chroot

```bash
apt-get install curl sudo ncurses-term
groupadd sudo
useradd -m -G sudo -s /bin/bash parch
passwd parch
```

- **note** : Replace parch with your username

2. add new user to sudoers

```bash
cat > /etc/sudoers << 'EOF'
root  ALL=(ALL) ALL
%sudo ALL=(ALL) ALL
EOF
```
3. connect to your user

```bash
sudo -iu parch
```
or
```bash
su parch
```

