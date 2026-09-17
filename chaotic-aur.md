---
title: استفاده از مخزن Chaotic AUR
description: استفاده از مخزن باینری های بیلد شده در مخزن AUR
published: true
date: 2026-07-03T13:37:12.222Z
tags: 
editor: markdown
dateCreated: 2026-05-25T08:09:43.628Z
---


برای استفاده از مخزن **Chaotic AUR** در پارچ لینوکس کافیست مخزن فعال برای Chaotic AUR داشته باشید.



  * در این آموزش ما از مخزن Whitelist شدهٔ freedif استفاده می‌کنیم تا در شرایط محدودیت های اینترنتی به مشکل بر نخوریم.

ابتدا فایل `/etc/pacman.conf` رو به کمک یک ادیتور (مثل `vim`، `nano` یا `micro`) باز می‌کنیم؛ سپس دو خط زیر را در انتهای فایل وارد می‌کنیم.
  *




    [chaotic-aur]
    Server = https://mirror.freedif.org/chaotic-aur/$repo/$arch

و فایل را ذخیره می‌کنیم و خارج می‌شویم.



سپس با استفاده از دستور


    sudo pacman -Syu

مخازن را به‌روزرسانی و سامانه را به‌روز می‌کنیم.



برای یافتن بسته‌های موجود، می‌توانید از دستور




    sudo pacman -Ss package_name

استفاده کنید.

