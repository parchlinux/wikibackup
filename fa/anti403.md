---
title: رفع تحریم‌ها با ابزار های مختلف
description: مخصوص کاربران ایرانی پارچ
published: true
date: 2024-07-28T14:18:02.896Z
tags: تحریم, پارچ, رفع‌تحریم
editor: markdown
dateCreated: 2024-07-28T14:17:52.101Z
---

# رفع تحریم
شاید برای شماهم پیش اومده باشه که موقع استفاده از یک ابزار خاص به شما خطای ۴۰۳ برگردونه. این خطا به معنی دسترسی غیرمجاز یا به عبارتی محدود شدن دسترسی شما با آی‌پی ایران به این ابزارها است.



## چگونگی رفع تحریم

### با استفاده از ساناد (DNS) 
برای رفع تحریم با استفاده از ساناد (سامانه نام دامنه) یا همان (DNS) شما می‌تونید از روش‌های زیر استفاده کنید:

#### تنظیم با استفاده از برنامه DNSCH

برای تنظیم ساناد با استفاده از برنامه‌های گفته شده، در ابتدا نیاز است که این برنامه‌ها را نصب کنید.

هردو برنامه در مخازن پارچ موجود هستند.
برای نصب dnsch:
```bash
sudo pacman -S dnsch
```
##### **نحوه استفاده از dnsch:**


تنظیم ساناد‌های مختلف
```
sudo dnsch {g|sh|ag|cf|403|bg|rd|el}
```

تنظیم ساناد سفارشی
```
sudo dnsch --set 1.2.3.4 1.2.3.4
```

حذف سانادها
```
sudo dnsch {-c|--clear}
```

دریافت پینگ از سانادهای مختلف
```
sudo dnsch {-p|--ping}
```
برگرداندن به پیشفرض سیستمی
```
sudo dnsch {-r|--restore}
```
#### با استفاده از نام‌بان:
برای نصب نام‌بان بر روی توزیع پارچ کافی هستش تا دستور زیر رو داخل پایانه (ترمینال) وارد کنید:

```bash
sudo pacman -S namban
```

##### استفاده از نام‌بان
نام بان یک محیط گرافیکی رو داره که استفاده ازش رو بسیار ساده‌تر می‌کنه. فقط کافی هستش تا برنامه‌رو اجرا کنید تا با محیط زیر روبرو بشید:
![نام‌بان.png](/نام‌بان.png)


### با استفاده از پروکسی

برای رفع تحریم با استفاده از پروکسی می‌توانید از برنامه‌هایی مثل وارپ پلاس، آبلیوین، نکوری، کاربراتور و هیدیفای استفاده کنید.

#### وارپ پلاس و آبلیوین

وارپ پلاس و آبلیوین دسترسی شمارو به شبکه وارپ کلودفلیر ساده تر می‌کند، در آبلیوین که دارای یک محیط گرافیکی هستش شما میتونید در محیط های گنوم و پلاسما به سادگی از این برنامه استفاده کنید، اگر نیازی به محیط گرافیکی ندارید میتونید از دستور وارپ پلاس به این منظور استفاده کنید.

##### نصب در پارچ
شما این دو برنامه رو باید از aur نصب کنید، برای نصب:
```bash
paru -S oblivion-desktop-bin warp-plus-bin --noconfirm
```
را در محیط پایانه خودتون اجرا کنید (بدون نیاز به sudo)

##### استفاده از آبلیوین و وارپ پلاس:
برای اجرای وارپ پلاس شما نیازمند باز کردن ترمینال‌(پایانه) خودتون هستید.

پرچم‌های دستور وارپ پلاس:
```
NAME
  warp-plus

FLAGS
  -4                       only use IPv4 for random warp endpoint
  -6                       only use IPv6 for random warp endpoint
  -v, --verbose            enable verbose logging
  -b, --bind STRING        socks bind address (default: 127.0.0.1:8086)
  -e, --endpoint STRING    warp endpoint
  -k, --key STRING         warp key
      --dns STRING         DNS address (default: 1.1.1.1)
      --gool               enable gool mode (warp in warp)
      --cfon               enable psiphon mode (must provide country as well)
      --country STRING     psiphon country code (valid values: [AT BE BG BR CA CH CZ DE DK EE ES FI FR GB HR HU IE IN IT JP LV NL NO PL PT RO RS SE SG SK UA US]) (default: AT)
      --scan               enable warp scanning
      --rtt DURATION       scanner rtt limit (default: 1s)
      --cache-dir STRING   directory to store generated profiles
      --tun-experimental   enable tun interface (experimental)
      --fwmark UINT        set linux firewall mark for tun mode (default: 4981)
      --reserved STRING    override wireguard reserved value (format: '1,2,3')
      --wgconf STRING      path to a normal wireguard config
  -c, --config STRING      path to config file
      --version            displays version number

```

بعد از اتصال میتونید از پروکسی های http و یا socks5 با این آیپی و پورت استفاده کنید:
```
127.0.0.1:8086
```

##### استفاده از آبلیوین:
کافی هستش تا برنامه رو اجرا کنید و سپس در محیط باز شده بر روی دکمه موجود بزنید بعد از مدتی برنامه به شبکه وارپ متصل می‌شود.
![آبلیوین.png](/آبلیوین.png)


##### استفاده از کاربراتور

کاربراتور یکی دیگر از برنامه‌های خوب برای اتصال به شبکه تور می‌باشد که به صورت پیشفرض در مخازن پارچ موجود است.
برای نصب:
```bash
sudo pacman -S carburetor
```

برای اجرا کافی هستش تا اون رو از منوی برنامه‌ها اجرا کنید تا با صحنه زیر روبرو بشید:
![کاربراتور.png](/کاربراتور.png)

بعد از اجرا شدن بر روی connect بزنید تا به شبکه تور وصل بشید، بعد از اتصال پورت های مربوط به پروکسی socks و http به شما نشان داده می‌شود، همچنین می‌توانید از منوی همبرگری پل های تور را برای اتصال بهتر ویرایش کنید. 
