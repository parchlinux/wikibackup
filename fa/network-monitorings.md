---
title: مانیتورینگ شبکه
description: در این قسمت با ابزارهای مانیتورینگ شبکه در لینوکس آشنا خوهید شد.
published: true
date: 2025-08-26T16:39:51.515Z
tags: bmon, iftop, nethogs, nload
editor: markdown
dateCreated: 2025-08-26T16:36:57.529Z
---

# مانیتورینگ شبکه
مانیتورینگ شبکه به فرآیند نظارت مستمر بر اجزای یک شبکه کامپیوتری (مانند روترها، سوئیچ‌ها، فایروال‌ها، سرورها و حتی کلاینت‌ها) برای اطمینان از عملکرد صحیح، تشخیص مشکلات، برنامه‌ریزی ظرفیت و امنیت شبکه گفته می‌شود.

## هدف اصلی
- شناسایی زودهنگام مشکلات قبل از تاثیرگذاری بر کاربران 
- جمع‌آوری داده برای تحلیل و بهینه‌سازی عملکرد شبکه 
- تضمین در دسترس بودن (Availability) سرویس‌ها 
- افزایش امنیت شبکه با تشخیص فعالیت‌های غیرعادی 

## مولفه‌های کلیدی مانیتورینگ شبکه
1.  در دسترس بودن (Availability Monitoring)
بررسی اینکه دستگاه‌های شبکه آپ هستند و پاسخ می‌دهند.
روش معمول: ارسال Ping و بررسی پاسخ.

2.  کارایی (Performance Monitoring)
اندازه‌گیری پهنای باند مصرفی (Bandwidth)
بررسی تأخیر (Latency) و از دست رفتن بسته‌ها (Packet Loss)
نظارت بر استفاده از CPU و حافظه دستگاه‌های شبکه

3. ترافیک شبکه (Traffic Monitoring)
تحلیل الگوهای ترافیک
شناسایی برنامه‌ها و کاربران پرمصرف
تشخیص ترافیک غیرعادی یا مخرب

4.  لاگ و گزارش‌گیری (Logging & Reporting)
ثبت رویدادها برای تحلیل آینده
تولید گزارش‌های دوره‌ای برای مدیریت

## پروتکل‌ها و تکنولوژی‌های رایج

1. SNMP (Simple Network Management Protocol)
پروتکل استاندارد برای جمع‌آوری اطلاعات از دستگاه‌های شبکه
استفاده از MIB (Management Information Base) برای تعریف داده‌های قابل دسترسی

2.  NetFlow / sFlow / IPFIX
پروتکل‌های برای جمع‌آوری اطلاعات مربوط به جریان ترافیک شبکه
مفید برای تحلیل الگوهای ترافیک و تشخیص anomalies

3. Packet Sniffing
ضبط و تحلیل بسته‌های شبکه برای عیب‌یابی دقیق
ابزارهایی مانند Wireshark و tcpdump

4. ICMP (Internet Control Message Protocol)
استفاده از Ping و Traceroute برای بررسی connectivity و مسیریابی

### انواع ابزارهای مانیتورینگ شبکه

###### iftop
iftop یک ابزار خط فرمان (command-line) برای مانیتورینگ ترافیک شبکه در لینوکس است که به صورت real-time پهنای باند مصرفی را نشان می‌دهد.

برای نصب از دستور زیر استفاده کنید:
```bash
`‍sudo pacman -S iftop`
```
پس از نصب با استفاده از دستور ‍‍‍`sudo iftop` وارد محیط نرم افزار شوید.

###### ساختار interface iftop
وقتی iftop را اجرا می‌کنید، صفحه به سه بخش اصلی تقسیم می‌شود:

۱. نوار بالایی (Header)
مقیاس زمانی برای نمودارها

نرخ انتقال داده (مثلاً: 1.0Kb, 2.0Kb)

مدت زمان اجرای برنامه

۲. بخش میانی (ترافیک جاری)
لیست اتصالات فعال

نرخ ارسال (TX) و دریافت (RX) داده

آدرس IP مبدأ و مقصد

۳. نوار پایینی (Footer)
آمار کلی ترافیک

مقیاس نمایش


###### پارامترهای مهم خط فرمان 
```bash
# مشخص کردن interface شبکه
sudo iftop -i eth0

# نمایش پورت‌ها
sudo iftop -P

# غیرفعال کردن DNS lookup
sudo iftop -n

# نمایش ترافیک بر حسب بایت (به جای بیت)
sudo iftop -B

# فیلتر کردن بر اساس پورت
sudo iftop -f "port 80"

# کمک و اطلاعات بیشتر
iftop --help

```

## Bmon

bmon (Bandwidth Monitor) یک ابزار مانیتورینگ پیشرفته و modular برای شبکه است که امکان مشاهده ترافیک شبکه به صورت رئال تایم با نمودارهای گرافیکی و امکانات گسترده را فراهم می‌کند.
روش ۱: نصب از طریق repos رسمی (توصیه شده):

```bash
به روز رسانی سیستم
sudo pacman -Syu

نصب bmon
sudo pacman -S bmon
```
روش ۲: نصب از طریق AUR (برای آخرین نسخه):

```bash
# با paru 
paru -S bmon

#  AUR helper
sudo pacman -S git base-devel
git clone https://aur.archlinux.org/bmon.git
cd bmon
makepkg -si
```
نحوه اجرا
```bash
# اجرای ساده
bmon

# اجرا با interface مشخص
bmon -p eth0

# اجرا با رزولوشن بالاتر
bmon -R

# نمایش help کامل
bmon -h
```

## nload
nload یک ابزار ساده اما قدرتمند برای مانیتورینگ ترافیک شبکه در لینوکس است که نمودارهای ASCII زیبا و خوانایی ارائه می‌دهد. بر خلاف iftop که اتصالات را نشان می‌دهد، nload بر نمایش کلی ترافیک هر interface تمرکز دارد.

روش ۱: نصب از طریق repos رسمی (توصیه شده)

```bash
# به روز رسانی سیستم
sudo pacman -Syu

# نصب nload
sudo pacman -S nload
```
روش ۲: نصب از طریق AUR
```bash
# yay با 
yay -S nload

# paru یا با 
paru -S nload
```

نحوه اجرا:

```bash
# اجرای ساده (همه interfaceها)
nload

# اجرا با interface مشخص
nload eth0

# نمایش help
nload -h
```
پارامترهای مهم خط فرمان
```bash
# مشخص کردن interface
nload wlan0

# نرخ آپدیت 500 میلی‌ثانیه
nload -t 500

# نمایش بر حسب بایت (به جای بیت)
nload -u B

# عدم نمایش نمودارها (فقط اعداد)
nload -n

# استفاده از اسکیل SI (کیلو=1000)
nload -S

# نمایش مجموع همه interfaceها
nload -a
```

نکات حرفه ای:

ترکیب با سایر ابزارها:
```bash
# نمایش nload و iftop همزمان
tmux new-session 'nload' \; split-window -v 'iftop'
```
مانیتورینگ خودکار:
```bash
# لاگ گیری از ترافیک هر 5 ثانیه
while true; do
    nload -t 5000 -n eth0 >> traffic.log
    sleep 5
done
```
## NetHogs 
NetHogs یک ابزار مانیتورینگ شبکه است که بر اساس پروسه (process) کار می‌کند. بر خلاف iftop که بر اساس اتصالات شبکه نمایش می‌دهد، NetHogs به شما نشان می‌دهد که کدام پروسه‌ها در حال مصرف پهنای باند هستند.

روش ۱: نصب از طریق repos رسمی (توصیه شده)
```bash
# به روز رسانی سیستم
sudo pacman -Syu

# نصب nethogs
sudo pacman -S nethogs
```

روش ۲: نصب از طریق AUR

```bash
# با yay
yay -S nethogs

# یا با paru
paru -S nethogs
```

نحوه اجرا:

```bash
# اجرای ساده (نیاز به sudo دارد)
sudo nethogs

# اجرا با interface مشخص
sudo nethogs wlan0

# نمایش help
nethogs -h
```

پارامترهای مهم خط فرمان

```bash
# مشخص کردن interface
sudo nethogs eth0

# نرخ آپدیت 3 ثانیه
sudo nethogs -d 3

# نمایش پورت‌ها
sudo nethogs -p

# نمایش نسخه
nethogs -V

# trace mode برای دیباگ
sudo nethogs -t
```

مثال‌های عملی

۱. شناسایی پروسه‌های پرمصرف:
```bash
sudo nethogs
```
۲. مانیتورینگ interface خاص با آپدیت سریع:
```bash
sudo nethogs -d 2 wlp3s0
```
۳. نمایش پورت‌ها:
```bash
sudo nethogs -p
```
۴. مانیتورینگ فقط TCP connections:
```bash
sudo nethogs -t
```