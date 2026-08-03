---
title: XAMPP
description: 
published: true
date: 2024-11-20T15:12:16.989Z
tags: xampp, php, آپاچی, پهپ
editor: markdown
dateCreated: 2024-11-20T13:44:50.986Z
---

# XAMPP
> XAMPP یک توزیع آپاچی با نصب آسان است که حاوی برنامه‌های MariaDB، PHP، Perl و ProFTPD می‌باشد، همچنین شامل برنامه های:
Apache, MariaDB, PHP & PEAR, Perl, ProFTPD, phpMyAdmin, OpenSSL, GD, Freetype2, libjpeg, libpng, gdbm, zlib, expat, Sablotron, libxml, Ming, Webalizer, pdf class, ncurses, mod_perl, FreeTDS, gettext, mcrypt, mhash, eAccelerator, SQLite و IMAP C-Client نیز می‌شود.

## نصب کردن
شما می‌توانید XAMPP را از AUR به کمک  paru در پارچ لینوکس نصب کنید:

```bash
paru -S xampp 
```

## کانفیگ کردن

کانفیگ پیش‌فرض باید خارج از جعبه کار کند. با ویرایش فایل های زیر می توانیم بخش های مختلف XAMPP را تنظیم کنیم: 

- ```/opt/lampp/etc/httpd.conf``` — کانفیگ آپاچی. برای مثال شما میتوانید پوشه حاوی فایل‌های متعلق به وب‌پیچ را عوض کنید.
- ```/opt/lampp/etc/php.ini``` — کانفیگ PHP.
- ```/opt/lampp/phpmyadmin/config.inc.php``` — کانفیگ phpMyAdmin.
- ```/opt/lampp/etc/proftpd.conf``` — کانفیگ ProFTPD.
- ```/opt/lampp/etc/my.cnf``` — کانفیگ MySQL.

اگر فقط می‌خواهید امنیت سرور را تنظیم کنید؛ این را اجرا کنید:
```bash
/opt/lampp/xampp security
```

## استفاده
برای کنترل XAMPP دستور آورده شده در زیر را وارد کنید:

```bash
/opt/lampp/xampp start,stop,restart
```

**به عنوان جایگزین**, شما می‌توانید سرویس ```xampp.service``` را شروع یا متوقف یا مجددا راه اندازی کنید.

