---
title: کی‌دی‌ای پلاسما
description: 
published: true
date: 2024-11-20T15:19:49.493Z
tags: پارچ, پلاسما, کی‌دی‌ای
editor: markdown
dateCreated: 2024-11-19T17:32:05.385Z
---

# کی‌دی‌ای پلاسما


## کی‌دی‌ای پلاسما چیست؟

کی‌دی‌ای پلاسما یک محیط میزکار یا ویژگی‌های زیاد و قابلیت شخصی‌سازی بالا است که تجربه کاربری مدرن و شهودی‌ای ارائه می‌دهد. همچنین برای انعطاف‌پذیری، گزینه‌های شخصی‌سازی زیاد و طیف گسترده‌ای از برنامه‌ها و ابزارها نیز شناخته شده است.
پارچ لینوکس پلاسما نسخه **پرچمدار** توزیع پارچ لینوکس است. 


![screenshot](https://raw.githubusercontent.com/parchlinux/parch-iso-plasma/main/image/screenshot.png)


## نصب کردن
شما می‌توانید با نصب پارچ لینوکس پلاسما یا با تغییر میزکار خود پلاسما را نصب کنید.
برای تغییر میزکار شما نیازمند نصب این بسته‌ها هستید:

```bash
sudo pacman -S plasma konsole kate dolphin sddm ark # for minimal installation

sudo pacman -S plasma konsole kate dolphin sddm ark plasmatube tokodon merkuro neochat marknote # for full ParchLinux plasma packages

```
> 
> اگر از آخرین نسخه گنوم مهاجرت می‌کنید؛ یادتان باشد `QT_QPA_PLATFORMTHEME=qt6ct` را از فایل `/etc/envierment` حذف کنید.
{.is-info}


## نکات و ترفندها

### گرفتن اسکرین شات از قسمتی

با فشار دادن <kbd>meta</kbd> + <kbd>shift</kbd> + <kbd>print</kbd> برنامه spectacle به شما اجازه می دهد قسمتی از صفحه برای اسکرین شات گرفتن انتخاب کنید.

### عوض کردن لوگوی منو به لوگوی پارچ لینوکس

تاکنون، ما لوگوی پارچ را بر روی منوی برنامه‌ها اعمال نکردیم. برای تغییر آن روی منو کلیک راست کنید و روی گزینه `Configure application menu` کلیک کنید سپس فایل `parch-logo.svg` را از این مکان انتخاب کنید:
`/usr/share/pixmaps/parch-logo.svg`

### انتخاب‌گر فایل کی‌دی‌ای برای فایرفاکس

برای اینکه فایرفاکس با کی‌دی‌ای بهتر کار کند, می‌توانید یا بسته `firefox-kde-opensuse`^AUR^ را نصب کنید، یا به طور دستی تنظیم کنید:


برای استفاده از انتخابگر فایل kde در فایرفاکس ۶۴ یا جدیدتر، بسته‌های `xdg-desktop-portal` و `xdg-desktop-portal-kde`, را نصب کنید؛ سپس فایرفاکس را باز کنید و در صفحه `about:config` مقدار `widget.use-xdg-desktop-portal.file-picker` را به ۱ تغییر دهید.