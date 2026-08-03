---
title: برنامه‌های کاربردی
description: لیستی از برنامه‌های کاربردی برای گنو/لینوکس بر اساس دسته‌بندی
published: true
date: 2025-09-02T18:11:41.890Z
tags: 
editor: markdown
dateCreated: 2025-07-29T16:26:48.677Z
---

# فهرستی از برنامه‌های کاربردی

این مقاله یک فهرست کلی از برنامه‌هاست که بر اساس دسته‌بندی مرتب شده و برای کسانی است که به دنبال بسته‌ها هستند. بسیاری از بخش‌ها بین برنامه‌های کنسولی و گرافیکی تقسیم شده‌اند. برنامه‌هایی که در بخش «کنسول» فهرست می‌شوند می‌توانند رابط گرافیکی هم داشته باشند، اما نسخه‌های رسمی فعلاً ذکر نشده‌اند.

> 💡 نکته:
> - می‌توانید بسته‌ی `pkgstats` را نصب کنید. این بسته یک تایمر `systemd` فراهم می‌کند که فهرست بسته‌های نصب‌شده روی سیستم شما به همراه معماری و میرورهای استفاده‌شده را ناشناس برای توسعه‌دهندگان آرچ لینوکس ارسال می‌کند تا در اولویت‌بندی‌ها کمک کند. داده‌ها قابل شناسایی نیستند. [صفحه‌ی آمار](https://pkgstats.archlinux.de/packages)  
> - بسته‌های Daemon معمولاً فایل واحد (unit) مربوط به systemd را برای شروع دارند. بعد از نصب می‌توانید با دستور زیر واحدها را ببینید:  
>   ```bash
>   pacman -Qql package | grep -Fe .service -e .socket
>   ```

---

## زیربخش‌ها
- [/اسناد](/fa/applications/documents)
- [/اینترنتی](/fa/applications/internet)
- [/چندرسانه‌ای](/fa/applications/multimedia)
- [/علمی](/fa/applications/science)
- [/امنیتی](/fa/applications/security)
- [/ابزارها](/fa/applications/utilities)
- [/سایر](/fa/applications/other)

---

## فهرست نرم‌افزارهای عمومی
- [پرتال: نرم‌افزار آزاد و متن‌باز](https://en.wikipedia.org/wiki/Portal:Free_and_open-source_software)
- [فهرست نرم‌افزارهای آزاد و متن‌باز](https://en.wikipedia.org/wiki/List_of_free_and_open-source_software_packages)
- [فهرست بسته‌های GNU](https://en.wikipedia.org/wiki/List_of_GNU_packages)
- [AlternativeTo](https://alternativeto.net/platform/linux/) — جایگزین‌های لینوکسی برای برنامه‌های پرکاربرد
- [Awesome Linux Software](https://github.com/luong-komorebi/Awesome-Linux-Software) — مجموعه‌ای از ابزارها و برنامه‌های لینوکسی
- [Linux Alternative Project](https://www.linuxalt.com/) — معادل‌های لینوکسی نرم‌افزارهای ویندوز
- [Linux Links Directory](https://www.linuxlinks.com/links/Software/) — دایرکتوری نرم‌افزارهای لینوکسی
- [Open Source Alternative](https://www.osalt.com/) — جایگزین‌های متن‌باز نرم‌افزارهای تجاری

---

## فهرست نرم‌افزارهای توزیع‌های دیگر
- [AppImageHub](https://appimage.github.io/)
- [Flathub](https://flathub.org/)
- [Snapcraft](https://snapcraft.io/)
- [بسته‌های Debian](https://packages.debian.org) + [اسکرین‌شات‌ها](https://screenshots.debian.net)
- [بسته‌های Fedora](https://packages.fedoraproject.org)
- [بسته‌های Gentoo](https://packages.gentoo.org/)
- [نرم‌افزار openSUSE](https://software.opensuse.org/)
- [بسته‌های Ubuntu](https://packages.ubuntu.com/)

---

## فهرست نرم‌افزارهای تخصصی
- [awesome-linuxaudio](https://github.com/nodiscc/awesome-linuxaudio) — نرم‌افزارهای تولید صدا/ویدئو/لایو
- [awesome-selfhosted](https://github.com/Kickball/awesome-selfhosted) — سرویس‌های شبکه و اپ‌های وب
- [awesome-shell](https://github.com/alebcay/awesome-shell) — فریم‌ورک‌ها و ابزارهای خط فرمان
- [awesome-sysadmin](https://github.com/n1trux/awesome-sysadmin) — نرم‌افزارهای مدیریت سیستم
- [برنامه‌های GNOME](https://apps.gnome.org/)
- [برنامه‌های KDE](https://apps.kde.org/)
- [Inconsolation](https://inconsolation.wordpress.com/index/) — بررسی نرم‌افزارهای مینیمال
- [K.Mandla's blog](https://kmandla.wordpress.com/software/) — اسکرین‌شات‌ها و بررسی اپ‌های کنسولی
- [Libre Projects](https://libreprojects.net/) — سرویس‌های وب متن‌باز
- [LinApp (آرشیو)](https://web.archive.org/web/20200530213904/http://lin-app.com/) — نرم‌افزار و بازی‌های تجاری لینوکس
- [PRISM Break](https://prism-break.org/en/all/) — نرم‌افزار علیه نظارت انبوه
- [Privacy Guides](https://www.privacyguides.org/en/tools/) — ابزارها و سرویس‌های حریم خصوصی بدون تبلیغ

---

## مَراکِز توسعه نرم‌افزار (Forges)
طبق [ویکی‌پدیا](https://en.wikipedia.org/wiki/Forge_(software)):
> Forge یک پلتفرم وب‌محور برای توسعه و اشتراک نرم‌افزار است.

- [Codeberg](https://codeberg.org/)
- [GitHub](https://github.com/explore)
- [GitLab](https://gitlab.com/explore)
- [Launchpad](https://launchpad.net/)
- [SourceHut](https://sourcehut.org/)
````
