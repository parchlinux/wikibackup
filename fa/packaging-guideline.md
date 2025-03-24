---
title: راهنمای بسته‌بندی برای توسعه‌دهندگان
description: 
published: true
date: 2025-03-24T19:10:52.380Z
tags: 
editor: markdown
dateCreated: 2024-11-22T10:28:31.070Z
---



## **راهنمای جامع بسته‌بندی در پارچ لینوکس**

### **1. مقدمه**
> این راهنما طراحی شده است تا استانداردهای لازم برای بسته‌بندی تمامی انواع نرم‌افزارها، ابزارها، فونت‌ها، برنامه‌های Wine و حتی برنامه‌های اندرویدی قابل اجرا در Waydroid را در توزیع پارچ لینوکس پوشش دهد. هدف ما ایجاد یکنواختی، پایداری، و کیفیت در بسته‌ها است.

---

### **2. پیش‌نیازها**

#### **ابزارهای اصلی ساخت بسته**
1. **ابزارهای ضروری:**
   - `base-devel`: شامل ابزارهایی مانند `gcc`, `make`, `patch`.
   - `git`: برای دریافت سورس‌ها از مخازن.
   - `waydroid` (برای تست برنامه‌های اندرویدی، در صورت نیاز).

2. **ابزارهای خاص:**
   - **برای Wine:** نصب `wine` و `winetricks`.
   - **برای Waydroid:** نصب Waydroid از مخازن رسمی (یا AUR).

3. **ساختار فایل PKGBUILD:**
   فایل PKGBUILD باید در بالاترین سطح شامل متغیرهای زیر باشد:
   - نام بسته (`pkgname`)، نسخه (`pkgver`)، شماره انتشار (`pkgrel`)، معماری (`arch`).
   - وابستگی‌ها (`depends`, `makedepends`)، لایسنس، توضیحات، و سورس.

#### **آشنایی با استاندارد FHS**
فایل‌ها باید طبق استاندارد **Filesystem Hierarchy Standard (FHS)** در مسیرهای مناسب قرار گیرند:
- **باینری‌ها:** `/usr/bin`
- **کتابخانه‌ها:** `/usr/lib` یا `/usr/lib64`
- **فونت‌ها:** `/usr/share/fonts/<نوع>`
- **داده‌های عمومی:** `/usr/share/<نام‌بسته>`
- **پیکربندی‌ها:** `/etc/<نام‌بسته>`

---

### **3. ساختار کلی PKGBUILD**

برای تمامی بسته‌ها، فایل PKGBUILD باید شامل این متغیرها باشد:

```bash
pkgname=<نام بسته>
pkgver=<نسخه>
pkgrel=<شماره انتشار>
pkgdesc="<توضیح مختصر بسته>"
arch=('x86_64' 'armv7h' 'aarch64') # یا هر معماری پشتیبانی‌شده
url="<آدرس پروژه>"
license=('GPL' 'MIT' 'custom')
depends=('فهرست بسته‌های وابسته')
makedepends=('فهرست ابزارهای لازم برای ساخت')
source=("آدرس سورس کد یا فایل")
sha256sums=('چک‌سام فایل‌ها')
```

---

### **4. بسته‌بندی فونت‌ها**

#### **قواعد نام‌گذاری:**
- **TrueType:** `ttf-fontname`
- **OpenType:** `otf-fontname`
- **Bitmap:** `bdf-fontname`

#### **مثال کامل برای فونت TrueType:**
بسته‌بندی فونت DejaVu:

```bash
pkgname=ttf-dejavu
pkgver=2.37
pkgrel=1
arch=('any')
pkgdesc="فونت‌های DejaVu با پشتیبانی گسترده."
license=('custom:Bitstream Vera')
source=("https://sourceforge.net/projects/dejavu/files/dejavu/${pkgver}/dejavu-fonts-ttf-${pkgver}.tar.bz2")
sha256sums=('fa9ca4efc0e2907e723aad11dc8f71c1f7b79be15f4f9b2c1214eeeaefa0f4dd')

package() {
    cd "${srcdir}/dejavu-fonts-ttf-${pkgver}"
    install -dm755 "${pkgdir}/usr/share/fonts/ttf-dejavu"
    install -m644 ttf/*.ttf "${pkgdir}/usr/share/fonts/ttf-dejavu/"
}
```

#### **تست و فعال‌سازی فونت:**
- پس از نصب بسته، اطمینان حاصل کنید که فایل‌های فونت با دستور `fc-cache` در دسترس هستند:
  ```bash
  post_install() {
      fc-cache -f
  }
  ```

---

### **5. بسته‌بندی برنامه‌های Wine**

#### **قواعد خاص برای Wine:**
- **نام‌گذاری:** برنامه‌های Wine باید به صورت `<نام-بسته>-wine` نام‌گذاری شوند.
  - مثال: `notepad-wine`, `winrar-wine`.
- **وابستگی‌ها:**
  - تمام بسته‌های Wine به `wine`, `winetricks`، و وابستگی‌های خاص خود نیاز دارند.
- **محل فایل‌ها:**
  - باینری‌های قابل اجرا باید در `/opt/<نام-بسته>` قرار گیرند.
  - در صورت نیاز به پیکربندی Wine، باید فایل‌های تنظیمات در `/etc/<نام-بسته>` ذخیره شوند.

#### **مثال PKGBUILD برای یک برنامه ساده در Wine:**
فرض کنیم می‌خواهید بسته **Notepad++** را در Wine بسته‌بندی کنید:

```bash
pkgname=notepadplusplus-wine
pkgver=8.5
pkgrel=1
arch=('x86_64')
pkgdesc="ویرایشگر متن Notepad++ برای اجرا تحت Wine"
license=('GPL')
depends=('wine' 'winetricks')
source=("https://github.com/notepad-plus-plus/notepad-plus-plus/releases/download/v${pkgver}/npp.${pkgver}.Installer.exe")
sha256sums=('d7e62d70d5d1dc0c4e31e9da57edb937d8a6e3c5457e405fc41d1e1dbb2b34cf')

package() {
    install -Dm755 "$srcdir/npp.${pkgver}.Installer.exe" "$pkgdir/usr/share/notepadplusplus/installer.exe"
    echo '#!/bin/bash' > "$pkgdir/usr/bin/notepadplusplus"
    echo 'wine /usr/share/notepadplusplus/installer.exe' >> "$pkgdir/usr/bin/notepadplusplus"
    chmod +x "$pkgdir/usr/bin/notepadplusplus"
}
```

---

### **6. بسته‌بندی برنامه‌های اندروید برای Waydroid**

#### **قواعد خاص برای Waydroid:**
- **نام‌گذاری:** بسته‌های اندرویدی باید به صورت `<نام-برنامه>-waydroid` نام‌گذاری شوند.
  - مثال: `whatsapp-waydroid`, `vlc-waydroid`.
- **فرمت APK:** فایل‌های APK به عنوان منبع بسته‌بندی استفاده می‌شوند.
- **وابستگی‌ها:** تمامی بسته‌ها به `waydroid` نیاز دارند.

#### **مثال PKGBUILD برای برنامه اندروید:**
فرض کنیم می‌خواهید برنامه WhatsApp را بسته‌بندی کنید:

```bash
pkgname=whatsapp-waydroid
pkgver=2.23.12.76
pkgrel=1
arch=('any')
pkgdesc="WhatsApp Messenger برای اجرا تحت Waydroid"
license=('custom')
depends=('waydroid')
source=("https://www.whatsapp.com/android/current/WhatsApp-${pkgver}.apk")
sha256sums=('4a5d8a6f2c54b6f6fa7e652ff8a5eb37c68a1299f65863b0af8b5d3ef4e3c91b')

package() {
    install -Dm644 "$srcdir/WhatsApp-${pkgver}.apk" "$pkgdir/usr/share/waydroid/apps/WhatsApp-${pkgver}.apk"
}
```

#### **نصب و اجرای APK در Waydroid:**
برای نصب خودکار برنامه، می‌توانید اسکریپتی اضافه کنید:
```bash
post_install() {
    waydroid app install /usr/share/waydroid/apps/WhatsApp-${pkgver}.apk
}
```

---

### **7. مدیریت وابستگی‌ها**

- **وابستگی‌های اجرا (depends):** بسته‌هایی که نرم‌افزار به آن‌ها نیاز دارد (مثل `wine`, `fontconfig`, `waydroid`).
- **وابستگی‌های ساخت (makedepends):** ابزارهایی که فقط برای ساخت بسته موردنیاز هستند (مثل `gcc`, `cmake`).

---

### **8. تست بسته‌ها**

1. **تست با `namcap`:**
   ```bash
   namcap PKGBUILD
   namcap <نام-بسته>.pkg.tar.zst
   ```

2. **تست اجرا روی Waydroid یا Wine:**
   - Waydroid:
     ```bash
     waydroid app install <نام-فایل-APK>
     waydroid app launch <نام-برنامه>
     ```
   - Wine:
     ```bash
     wine /opt/<نام-برنامه>/<فایل-اجرایی>
     ```

---

### **9. ارسال بسته‌ها به مخازن**

- در گیت پارچ حساب بسازید
- بسته‌خود را با توجه به بسته‌بندی های موجود در مخزن pkgbuilds پارچ به صورت یک درخواست ادغام ارائه دهید.
- تا تأیید و تست‌های تیم پارچ صبر کنید.
- پس از تأیید توسط تیم پارچ بسته شما با توجه به نوع در یکی از مخازن ppr و pcp بارگذاری می‌شود