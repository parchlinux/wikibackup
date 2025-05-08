---
title: XAMPP
description: 
published: true
date: 2025-05-08T11:22:18.562Z
tags: xampp, apache, php
editor: markdown
dateCreated: 2025-05-08T11:22:18.562Z
---

# XAMPP
> XAMPP ist eine leicht zu installierende Apache-Distribution, die MariaDB, PHP, Perl und ProFTPD enthält. Folgende Komponenten sind enthalten: Apache, MariaDB, PHP & PEAR, Perl, ProFTPD, phpMyAdmin, OpenSSL, GD, FreeType2, libjpeg, libpng, gdbm, zlib, expat, Sablotron, libxml, Ming, Webalizer, PDF-Klasse, ncurses, mod_perl, FreeTDS, gettext, mcrypt, mhash, eAccelerator, SQLite und IMAP-C-Client. 


## Installation

Sie können XAMPP aus dem AUR mit Paru in Arch Linux installieren.

```bash
paru -S xampp 
```

## Konfiguration

Die Standardkonfiguration sollte direkt funktionieren. Die Anpassung der einzelnen Komponenten von XAMPP kann durch die Bearbeitung der folgenden Dateien vorgenommen werden: 

- ```/opt/lampp/etc/httpd.conf``` — Apache-Konfiguration. Zum Beispiel können Sie den Ordner ändern, der die Quelldateien der Webseite enthält.
- ```/opt/lampp/etc/php.ini``` — PHP konfiguration.
- ```/opt/lampp/phpmyadmin/config.inc.php``` — phpMyAdmin konfiguration.
- ```/opt/lampp/etc/proftpd.conf``` — ProFTPD konfiguration.
- ```/opt/lampp/etc/my.cnf``` — MySQL konfiguration.

Wenn Sie die Server-Sicherheit einrichten möchten, führen Sie den folgenden Befehl aus:
```bash
/opt/lampp/xampp security
```

## Verwendung

Verwenden Sie die folgenden Befehle, um XAMPP zu steuern:

```bash
/opt/lampp/xampp start,stop,restart
```

**Alternativ** können Sie ```xampp.service``` starten, stoppen oder neu starten.

