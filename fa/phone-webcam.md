---
title: استفاده از دستگاه اندرویدی به عنوان وب‌کم
description: 
published: true
date: 2024-07-29T18:44:58.943Z
tags: پارچ, وب‌کم, اندروید
editor: markdown
dateCreated: 2024-07-29T18:44:09.325Z
---

# چگونه از تلفن اندرویدی به عنوان وب‌کم در پارچ استفاده کنیم؟


## نصب پیش‌نیاز ها

اول از همه باید چند پیش‌نیاز را نصب کنید:

```bash
sudo pacman -S scrcpy dkms base-devel linux-headers v4l2loopback-dkms
```

سپس باید ماژول را بارگذاری کنید:

```bash
sudo modprobe v4l2loopback exclusive_caps=1
```

## استفاده

### به اشتراک گذاری دوربین

برای استفاده از دوربین جلو ابتدا **usb debugging** را در گوشی خود فعال کنید، سپس گوشی خود را از طریق کابل به رایانه وصل کنید و این دستور را در ترمینال اجرا کنید:

```bash
scrcpy --video-source=camera --camera-size=1920x1080 --camera-facing=front --v4l2-sink=/dev/video0 --no-playback --no-window
```

برای دوربین پشتی، کافی است ```--camera-facing=front``` را به ```--camera-facing=back``` تغییر دهید.

#### تست دوربین

 obs را باز کنید یا این دستور را اجرا کنید:

```bash
ffplay /dev/video0
```

### به اشتراک گذاری میکروفون

برای میکروفون می توانید این دستور را اجرا کنید:

```bash
scrcpy --no-video --audio-source=mic --no-window
```

این دستور میکروفون تلفن شما را به عنوان صدای سیستم به اشتراک می گذارد.