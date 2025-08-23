---
title: زنجیره‌پروکسی
description: ابزاری ساده است که پروکسی‌های معمولی شما را به یک تونل تبدیل می‌کند
published: true
date: 2025-08-23T14:09:33.922Z
tags: نکات
editor: markdown
dateCreated: 2025-08-18T03:49:35.109Z
---

# راهنمای استفاده از زنجیره‌پروکسی (ProxyChains) - تونل‌سازی شبکه

زنجیره‌پروکسی ابزاری است که امکان عبور ترافیک شبکه از طریق یک یا چند پروکسی را فراهم می‌کند. این ابزار پروکسی‌های SOCKS4، SOCKS5 و HTTP را پشتیبانی می‌کند.

## نصب در پارچ

```bash
sudo paru -S proxychains-ng
```

## راه‌اندازی اولیه

ابتدا باید فایل تنظیمات را کپی کنید:

```bash
cp /etc/proxychains.conf ~/.proxychains.conf
```

حالا فایل تنظیمات شخصی شما در مسیر خانه ایجاد شد. برای باز کردن و ویرایش آن:

```bash
nano ~/.proxychains.conf
```

## تنظیم حالت زنجیره

در فایل باز شده، خطوط زیر را پیدا کنید:

```conf
#dynamic_chain
#strict_chain
#random_chain
```

یکی از آنها را انتخاب کنید و علامت `#` از ابتدای آن بردارید. برای مبتدی‌ها `dynamic_chain` توصیه می‌شود:

```conf
dynamic_chain
#strict_chain
#random_chain
```

### توضیح حالت‌ها:

- `strict_chain`: همه پروکسی‌ها باید کار کنند
- `dynamic_chain`: پروکسی‌های خراب رد می‌شوند  
- `random_chain`: هر بار یکی تصادفی انتخاب می‌شود

## تنظیم DNS

خط زیر را پیدا کنید و مطمئن شوید علامت `#` ندارد:

```conf
proxy_dns
```

## اضافه کردن پروکسی‌ها

در انتهای فایل، قسمت `[ProxyList]` را پیدا کنید. خطوط نمونه را پاک کنید و پروکسی خودتان را اضافه کنید:

```conf
[ProxyList]
# نوع    آدرس        پورت   نام‌کاربری   رمزعبور

socks5  127.0.0.1    1080
socks5  myproxy.com  1080   myuser      mypass
```

### ذخیره و خروج از nano

1. `Ctrl + O` برای ذخیره
2. `Enter` برای تأیید نام فایل
3. `Ctrl + X` برای خروج

## استفاده

### تست اولیه

ابتدا IP عادی خود را ببینید:

```bash
curl http://ipinfo.io/ip
```

حالا همان دستور را با proxychains اجرا کنید:

```bash
proxychains curl http://ipinfo.io/ip
```

اگر IP متفاوت بود، یعنی کار می‌کند!

### استفاده با مرورگر

```bash
proxychains zen-browser
```

### استفاده با دیگر برنامه‌ها

```bash
proxychains wget http://example.com/file.zip
proxychains ssh user@server.com
```

## مثال کامل فایل تنظیمات

اگر نمی‌دانید چطور تنظیم کنید، می‌توانید فایل خود را پاک کنید و این نمونه را کپی کنید:

```bash
rm ~/.proxychains.conf
nano ~/.proxychains.conf
```

سپس این محتوا را کپی کنید:

```conf
dynamic_chain
proxy_dns
tcp_read_time_out 15000
tcp_connect_time_out 8000

[ProxyList]
# پروکسی خود را اینجا بنویسید:
# socks5  آدرس_پروکسی  پورت  نام_کاربری  رمزعبور

socks5  127.0.0.1  1080
```

`Ctrl + O` سپس `Enter` سپس `Ctrl + X` برای ذخیره و خروج.



