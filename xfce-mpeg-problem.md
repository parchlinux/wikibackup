---
title: رفع خطای کدک MPEG در XFCE
description: 
published: true
date: 2025-10-16T10:04:45.949Z
tags: 
editor: markdown
dateCreated: 2025-10-16T10:04:45.949Z
---

### رفع خطای عدم پشتیبانی از کُدک MPEG در XFCE

اگر تازه محیط **XFCE** را در **Parch Linux** نصب کرده باشید، ممکن است هنگام پخش ویدیو با خطای زیر مواجه شوید:

```
VLC could not decode the format “mpgv” (MPEG-1/2 Video)
Codec not supported:
```

این خطا معمولاً در نشست (session) مربوط به XFCE مشاهده می‌شود، زیرا سایر نشست‌ها ممکن است به‌درستی بارگذاری نشوند یا صفحه سیاه نمایش دهند.

برای رفع این مشکل، کافی است بسته‌ی **ffmpeg** را نصب کنید. در ترمینال دستور زیر را اجرا کنید:

```bash
sudo pacman -S ffmpeg
```

اگر پیش‌تر **VLC** را نصب کرده‌اید، توصیه می‌شود آن را حذف و مجدداً نصب کنید تا با ffmpeg یکپارچه شود:

```bash
sudo pacman -S vlc
```

برای اطمینان از نصب صحیح کُدک‌ها، می‌توانید پخش ویدیو را با ابزار **ffplay** (از بسته‌ی ffmpeg) آزمایش کنید:

```bash
ffplay yourvideo.mp4
```

به‌جای `yourvideo.mp4`، نام فایل ویدیوی خود را بنویسید.