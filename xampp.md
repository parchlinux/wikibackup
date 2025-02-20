---
title: XAMPP
description: 
published: true
date: 2024-07-26T09:34:57.689Z
tags: xampp, apache, php
editor: markdown
dateCreated: 2024-07-26T09:34:43.803Z
---

# XAMPP
> XAMPP is an easy to install Apache distribution containing MariaDB, PHP, Perl and ProFTPD. It contains: Apache, MariaDB, PHP & PEAR, Perl, ProFTPD, phpMyAdmin, OpenSSL, GD, Freetype2, libjpeg, libpng, gdbm, zlib, expat, Sablotron, libxml, Ming, Webalizer, pdf class, ncurses, mod_perl, FreeTDS, gettext, mcrypt, mhash, eAccelerator, SQLite and IMAP C-Client. 


## Installation

You can install XAMPP from aur using Paru in Parch Linux:

```bash
paru -S xampp 
```

## Configuration

The default configuration should work out of the box. Setting the individual parts of XAMPP can by made by editing following files: 

- ```/opt/lampp/etc/httpd.conf``` — Apache configuration. For example you can change folder with web page's source files.
- ```/opt/lampp/etc/php.ini``` — PHP configuration.
- ```/opt/lampp/phpmyadmin/config.inc.php``` — phpMyAdmin configuration.
- ```/opt/lampp/etc/proftpd.conf``` — ProFTPD configuration.
- ```/opt/lampp/etc/my.cnf``` — MySQL configuration.

If you would like to set up security of server, just run:
```bash
/opt/lampp/xampp security
```

## Usage
Use the following commands to control XAMPP: 

```bash
/opt/lampp/xampp start,stop,restart
```

**Alternatively**, you can start, stop, or restart ```xampp.service```.

