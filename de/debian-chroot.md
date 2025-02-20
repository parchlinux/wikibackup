---
title: Debian Chroot im Parch Linux
description: Eine Anleitung zur Nutzung von Debian unter Parch Linux
published: true
date: 2024-10-18T07:33:28.930Z
tags: debian, parch
editor: markdown
dateCreated: 2024-10-18T07:33:24.452Z
---

# Was ist ein Chroot?
Die Linux-Utility chroot kann das Arbeitsverzeichnis eines Prozesses ändern und den Zugriff auf den Rest des Dateisystems einschränken.

## wie erhält man ein Debian-Chroot in ParchLinux?

1. Installieren Sie Debootstrap

```bash
sudo pacman -Sy
sudo pacman -S debootstrap
```

2. Erstellen Sie einen Ordner in /opt für Ihr neues Debian root

```bash
sudo mkdir /opt/debian
```

3. Legen Sie den Debootstrap-Speicherort fest und starten Sie das Debootstraping :D

```bash
DEBOOTSTRAP_DIR=/opt/debootstrap/usr/share/debootstrap /opt/debootstrap/usr/sbin/debootstrap --arch amd64 bookworm /opt/debian/ http://ftp.uk.debian.org/debian/
```

- **Hinweis**: Sie können die Debian-Version ändern, indem Sie den Bookworm in Ihren Versionscodenamen ändern. Sie finden Debian-Codenamen [hier](https://wiki.debian.org/DebianReleases#Production_Releases).

4. Mounten Sie die Verzeichnisse

```bash
mount -t proc proc /opt/debian/proc/
mount -t sysfs sys /opt/debian/sys/
mount -o bind /dev /opt/debian/dev/
mount -o bind /dev/pts /opt/debian/dev/pts/
```

5. Richten Sie die Repositories für Ihr Chroot-System ein

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

- **Hinweis**: Ändern Sie den Codenamen in Ihre installierte Version

6. Chroot zu Ihrem Debian

```bash
chroot /opt/debian /bin/bash
```

7. Aktualisieren Sie Debian und generieren Sie die Gebietsschemas neu:

```bash
apt-get update && apt-get dist-upgrade
apt-get install locales
dpkg-reconfigure locales
```

8. Fügen Sie einen Namen hinzu /etc/hosts

```bash
echo mywonderfulldebian >> /etc/hosts
```

## Optional

1. Einen neuen Benutzer zum Chroot hinzufügen

```bash
apt-get install curl sudo ncurses-term
groupadd sudo
useradd -m -G sudo -s /bin/bash parch
passwd parch
```

- **Hinweis**: Ersetzen Sie „parch“ durch Ihren Benutzernamen.

2. neuen Benutzer zu sudoers hinzufügen

```bash
cat > /etc/sudoers << 'EOF'
root  ALL=(ALL) ALL
%sudo ALL=(ALL) ALL
EOF
```
3. Stellen Sie eine Verbindung zu Ihrem Benutzer her

```bash
sudo -iu parch
```
oder
```bash
su parch
```

