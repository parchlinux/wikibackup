---
title: Adobe Connect
description: 
published: true
date: 2026-06-09T19:28:33.884Z
tags: 
editor: markdown
dateCreated: 2026-05-17T16:44:56.209Z
---

**Adobe Connect** نرم افزاری حرفه ای جهت راه اندازی کنفرانس و کلاس مجازی آنلاین میباشد.

# برخی قابلیت های نرم افزار Adobe Connect

* راه اندازی webinar
* مدیریت کاربران در وب کنفرانس
* آپلود کردن تصاویر
* آپلود کردن و نمایش PowerPoint
* دارای تخته وایت برد جهت نوشتن بر روی آن و نمایش به سایرین
* چت کردن با شرکت کنندگان در کنفرانس یا کلاس
* کنفرانس صوتی جهت آموزش مجازی
* کنفرانس تصویری جهت آموزش مجازی
* به اشتراک گذاشتن صفحه دسکتاپ برای سایر شرکت کنندگان
* ضبط کنفرانس ها و به اشتراک گذاشتن فایل ویدیویی
* برگزاری نظر سنجی

## مشکل اصلی Adobe Connect در گنو/لینوکس
 این ابزار فقط برای Microsoft Windows و MacOS عرضه شده و شما برای استفاده از باید از نسخه وب استفاده کنید.

# حل مشکلات ادوبی کانکت در گنو/لینوکس
نسخه وب ادوبی کانکت در گنو/لینوکس دارای مشکلاتی است که در این صفحه مجموعه‌ای از نکات کاربردی و ترفندهای پیشرفته برای استفاده از نسخه وب ذکر میکنیم:
## عدم ورود به کلاس

برای حل این موضوع نیاز به افزونه User-Agent Switcher and Manager برای تغییر شناسهٔ مرورگر (User-Agent) به مرورگری که ادوبی کانکت آن را تأیید می‌کند دارید.

### افزونه User-Agent Switcher and Manager

<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>افزونه User-Agent Switcher and Manager بر اساس مرورگر ها</title>
  <style>
    table {
      border-collapse: collapse;
      width: 100%;
      max-width: 500px;
      margin: 20px auto;
      font-family: Tahoma, sans-serif;
    }

    caption {
      font-weight: bold;
      margin-bottom: 10px;
      font-size: 1.1em;
    }

    th, td {
      padding: 10px 12px;
      text-align: center;
      border: 1px solid #ccc;
    }

    th {
      background-color: #f0f0f0;
      font-weight: bold;
    }

    tr:nth-child(even) {
      background-color: #fafafa;
    }
  </style>
</head>
<body>
  <table>
    <thead>
      <tr>
        <th scope="col">مرورگر</th>
        <th scope="col">افزونه</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Firefox</td>
        <td><a href="https://addons.mozilla.org/en-US/firefox/addon/user-agent-string-switcher">Extension for Firefox</a></td>
      </tr>
      <tr>
        <td>Chrome</td>
        <td><a href="https://chromewebstore.google.com/detail/user-agent-switcher-and-m/bhchdcejhohfmigjafbampogmaanbfkg">Extension for Chrome</a></td>
      </tr>
    </tbody>
  </table>
</body>
</html>

## عدم اشتراک‌گذاری صفحه در نسخه وب ادوبی کانکت

در نسخه‌ی تحت وب Adobe Connect، امکانات اشتراک‌گذاری صفحه به صورت پیش‌فرض وجود ندارد و تنها می‌توان میکروفون، فایل یا وب‌کم را به اشتراک گذاشت. با روشی که در ادامه توضیح داده می‌شود، می‌توانید صفحه‌ی خود را به عنوان یک وب‌کم مجازی به جلسه ارسال کنید. این روش در سیستم‌عامل گنو/لینوکس (با استفاده از بسته‌های obs-studio و v4l2loopback) اجرا شده و روی پلتفرم‌های مشابه (مانند بیگ بلو باتن) نیز کار می‌کند.

### مراحل اجرا
در ترمینال، دستور زیر را برای دریافت ابزار ها اجرا کنید:

```
sudo pacman -S obs-studio v4l2loopback-dkms
```

برای بارگذاری ماژول v4l2loopback با پارامترهای خاص دستور زیر را وارد کنید:

```
sudo modprobe v4l2loopback video_nr=10 card_label="OBS Virtual Camera" exclusive_caps=1
```

اکنون در مرورگر، در جلسه‌ی Adobe Connect (یا هر برنامه‌ی ویدئوکنفرانسی) می‌توانید دوربین مجازی «OBS Virtual Camera» را انتخاب کنید. آنچه در OBS نمایش داده می‌شود، به‌عنوان خروجی دوربین به جلسه ارسال خواهد شد.