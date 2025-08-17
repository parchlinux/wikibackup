---
title: wine
description: لایه سازگاری برنامه‌های ویندوزی با گنو/لینوکس
published: true
date: 2025-08-17T20:06:28.815Z
tags: لینوکس, واین
editor: markdown
dateCreated: 2024-11-10T16:18:20.333Z
---

# واین
واین (WINE) که مخفف بازگشتی wine is not an emulator هستش یک لایه سازگاری برای اجرای برنامه‌های ویندوزی بر روی گنو/لینوکس می‌باشد.

## نصب بر روی پارچ

برای نصب واین بر روی پارچ کافی هستش تا ترمینال رو باز کنید و این دستور رو داخلش بزنید:
```bash
sudo pacman -S wine wine-mono wine-gecko
```

## استفاده از واین

برای استفاده از واین کافیه تا اول دستور ```winecfg``` رو داخل ترمینال اجرا کنید و بعد از انجام دادن تنظیمات اولیه با دستور
```
wine program.exe
```
برنامه مورد نظرتون رو اجرا کنید.

>**هشدار** 
لایه سازگاری واین با اکثر برنامه‌ها ممکنه به خوبی  کار نکنه پس قبل از نصب یک برنامه از سازگاری اون با واین اطمینان حاصل کنید.
{.is-warning}

## برنامه‌های گرافیکی برای مدیریت واین
>**نکته**
بعضی از برنامه‌ها از AUR نصب می‌شوند، اطمینان حاصل کنید که ابتدا آموزش استفاده از [مدیربسته](https://wiki.parchlinux.com/fa/Package-management) را مطالعه کرده باشید.
{.is-info}

>**هشدار**
این ابزارها دارای جوامع و وب‌سایت‌های اختصاصی خود هستند و توسط جامعه اصلی Wine پشتیبانی نمی‌شوند.
{.is-warning}


### Bottles
مدیر گرافیکی برای مدیریت پریفیکس‌ها و رانرهای Wine که بر پایه GTK ساخته شده است.

- [وب‌سایت Bottles](https://usebottles.com)
- بسته AUR: [bottles](https://aur.archlinux.org/packages/bottles)

### CrossOver
نسخه رسمی پولی Wine که یک رابط گرافیکی و پشتیبانی کامل‌تری برای کاربران فراهم می‌کند.

- [وب‌سایت CrossOver](https://www.codeweavers.com/crossover)
- بسته AUR: [crossover](https://aur.archlinux.org/packages/crossover)

### Lutris
لانچر بازی برای انواع بازی‌ها، از جمله بازی‌های Wine (با مدیریت پریفیکس)، بازی‌های بومی لینوکس و شبیه‌سازها.

- [وب‌سایت Lutris](https://lutris.net)
- بسته AUR: [lutris](https://aur.archlinux.org/packages/lutris)

### PlayOnLinux
مدیر گرافیکی پریفیکس برای Wine. دارای اسکریپت‌هایی برای نصب و پیکربندی برنامه‌ها.

- [وب‌سایت PlayOnLinux](https://www.playonlinux.com)
- بسته AUR: [playonlinux](https://aur.archlinux.org/packages/playonlinux)

### Proton
ابزاری برای سازگاری که برای Steam طراحی شده و بر پایه Wine و اجزای اضافی است. برای مشاهده لیست سازگاری به ProtonDB مراجعه کنید.

- [مخزن GitHub Proton](https://github.com/ValveSoftware/Proton)
- بسته AUR: [proton](https://aur.archlinux.org/packages/proton)

### PyWinery
یک مدیر ساده گرافیکی برای پریفیکس‌های Wine.

- [مخزن GitHub PyWinery](https://github.com/ergoithz/pywinery)
- بسته AUR: [pywinery](https://aur.archlinux.org/packages/pywinery)

### Q4Wine
مدیر گرافیکی پریفیکس برای Wine. می‌تواند تم‌های Qt را در تنظیمات Wine برای ادغام بهتر اعمال کند.

- [وب‌سایت Q4Wine](https://sourceforge.net/projects/q4wine/)
- بسته AUR: [q4wine-git](https://aur.archlinux.org/packages/q4wine-git)

### WINEgui
رابط گرافیکی کاربرپسند برای WINE.

- [مخزن GitLab WINEgui](https://gitlab.melroy.org/melroy/winegui)
- بسته‌های AUR: [winegui](https://aur.archlinux.org/packages/winegui)، [winegui-bin](https://aur.archlinux.org/packages/winegui-bin)

