---
title: chroot دبیان در پارچ لینوکس
description: 
published: true
date: 2024-04-05T14:06:30.798Z
tags: 
editor: markdown
dateCreated: 2024-04-05T13:51:42.264Z
---

# chroot چیست؟
ابزار لینوکس chroot می تواند دایرکتوری روت درحال کار را برای یک فرآیند تغییر دهد و دسترسی به بقیه فایل سیستم را محدود کند.
## چگونه chroot دبیان را داخل پارچ لینوکس داشته باشیم؟
1. Debootstrap را نصب کنید

```bash
sudo pacman -Sy
sudo pacman -S debootstrap
```
2. یک پوشه جدید داخل /opt دبیان خود بسازید
```bsah
sudo mkdir /opt/debian
```
3. مکان Debootstrap را تنظیم کنید و Debootstraping را شروع کنید

```bash
DEBOOTSTRAP_DIR=/opt/debootstrap/usr/share/debootstrap /opt/debootstrap/usr/sbin/debootstrap --arch amd64 bookworm /opt/debian/ http://ftp.uk.debian.org/debian/
```

- توجه: می توانید نسخه دبیان را با تغییر bookworm به کد نام دبیان خود تغییر دهید. در [اینجا](https://wiki.debian.org/DebianReleases#Production_Releases) می توانید کدهای اسم دبیان را پیدا کنید.
4. ماونت دایرکتوری ها
```bash
mount -t proc proc /opt/debian/proc/
mount -t sysfs sys /opt/debian/sys/
mount -o bind /dev /opt/debian/dev/
mount -o bind /dev/pts /opt/debian/dev/pts/
```
5. تنظیم مخازن برای سیستم chroot شده ی شما
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
- توجه: کد نام را به نسخه نصب شده خود تغییر دهید
6. به دبیان خود chroot بزنید 
```bash
chroot /opt/debian /bin/bashchroot /opt/debian /bin/bash
```
7. دبیان خود را بروز کنید و مکان ها را بازسازی کنید
```bash
apt-get update && apt-get dist-upgrade
apt-get install locales
dpkg-reconfigure locales
```
8. یک اسم به /etc/hosts اضافه کنید
```bash
echo mywonderfulldebian >> /etc/hosts
```
## اختیاری
1. یک کاربر جدید به chroot اضافه کنید
```bash
apt-get install curl sudo ncurses-term
groupadd sudo
useradd -m -G sudo -s /bin/bash parch
passwd parch
```
- توجه: نام کاربری خود را جایگزین parch کنید
2. کاربر جدید به sudoers اضافه کنید
```bash
cat > /etc/sudoers << 'EOF'
root  ALL=(ALL) ALL
%sudo ALL=(ALL) ALL
EOF
```
3. به کاربر خود متصل شوید
```bash
sudo -iu parch
```
یا
```bash
su parch
```