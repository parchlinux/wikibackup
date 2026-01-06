---
title: استفاده از انویدیا در پارچ
description: 
published: true
date: 2026-01-06T09:29:54.438Z
tags: پارچ, انویدیا
editor: markdown
dateCreated: 2024-11-13T18:31:50.299Z
---

## استفاده از گرافیک انویدیا در پارچ

با گفته‌های بزرگان و کاربران گنو/لینوکس، کارت گرافیک انویدیا در لینوکس دردسرهای فراوانی دارد و شبیه یک غول ترسناک به نظر می‌رسد اما امروز اینجاییم که این غول بزرگ را محو کنیم!

## نصب درایور

### درایور انحصاری انویدیا

پیش از هرکاری، ابتدا باید تشخیص دهیم که چه نسخه‌ای از درایور با گرافیک ما سازگار است بنابراین باید برنامه nvidia-helper را از مخازن پارچ نصب کنیم و آن را اجرا کنیم:

```bash
sudo pacman -S nvidia-helper && sudo nvidia-helper
```

اگر این خروجی را گرفتیم یعنی می‌توانیم آخرین نسخه درایور را نصب کنیم:

```
Your card is supported by the latest drivers.
It is recommended to install the nvidia package or install the nvidia-dkms package for custom kernels
```

#### مراحل نصب:

۱. ابتدای امر به کمک ویرایشگر نانو فایل `/etc/mkinitcpio.conf` را باز کنید:

```bash
sudo nano /etc/mkinitcpio.conf
```

۲. به این صورت بخش MODULES را پر کنید:

```
MODULES=(nvidia nvidia_modeset nvidia_uvm nvidia_drm)
```

۳. بعد از این کار از بخش `HOOKS` در همان فایل، کلمه kms را حذف کنید؛ به کمک میانبر <kbd>Ctrl + o</kbd> و سپس زدن اینتر فایل را ذخیره نموده و با میانبر <kbd>Ctrl + x</kbd> از ویرایشگر خارج شوید.

۴. در آخر به کمک دستور زیر درایور و اجزای آن را نصب نمایید:

```bash
sudo pacman -S nvidia nvidia-utils nvidia-settings
```

> **نکته**
> اگر شما کرنل کاستوم نصب کرده‌اید باید درایور nvidia-dkms را نصب کنید:
> ```bash
> sudo pacman -S nvidia-dkms nvidia-utils nvidia-settings
> ```
> اگر کرنل lts دارید:
> ```bash
> sudo pacman -S nvidia-lts nvidia-utils nvidia-settings
> ```
>{.is-info}

اما اگر یکی از خروجی‌های زیر را گرفتید با توجه به نام درایوری که برایتان نوشته شده یکی از درایورها را نصب کنید:

```
Your card is supported by the Tesla(470xx) dkms drivers.
Your card is supported by the legacy 390xx drivers.
Your card is supported by the legacy 340xx drivers.
```

به کمک دستورات:

```bash
paru -S nvidia-470xx-dkms nvidia-470xx-settings
# یا
paru -S nvidia-390xx-dkms nvidia-390xx-settings
# یا
paru -S nvidia-340xx-dkms nvidia-340xx-settings
```

### نصب درایور آزاد

در گنو/لینوکس، دو درایور آزاد برای گرافیک‌های انویدیا داریم:

#### ۱. nouveau

این درایور به‌صورت پیش‌فرض در کرنل موجود است و نیازمند نصب چیز دیگری نیست. اما مشکلات بسیار زیادی از جمله عدم کنترل سرعت فن و عملکرد ضعیف دارد؛ بنابراین توصیه نمی‌شود.

#### ۲. nvidia-open

از نسخه ۵۱۰ به بعد، درایور nvidia-open منتشر شد که کد کرنل آن باز است و از گرافیک‌های سری تورینگ (Turing) به بالا پشتیبانی می‌کند. [اینجا](https://github.com/NVIDIA/open-gpu-kernel-modules?tab=readme-ov-file#compatible-gpus) لیست گرافیک‌هایی است که از این درایور پشتیبانی می‌کنند.

> **توجه**
> درایور nvidia-open توسط انویدیا توصیه شده و برای کارت‌های سری تورینگ و جدیدتر مناسب است.
{.is-info}

نحوه نصب آن به این شکل است، ابتدا باید به کمک ویرایشگر نانو فایل `/etc/mkinitcpio.conf` را باز کنیم:

```bash
sudo nano /etc/mkinitcpio.conf
```

سپس بخش MODULES را این‌گونه پر کنید:

```
MODULES=(nvidia_modeset nvidia_uvm nvidia_drm)
```

بعد از این کار از بخش `HOOKS` همان فایل، کلمه kms را حذف کنید؛ به کمک میانبر <kbd>Ctrl + o</kbd> و سپس زدن اینتر فایل را ذخیره نموده و با میانبر <kbd>Ctrl + x</kbd> از ویرایشگر خارج شوید.

در آخر درایور و مشتقات آن را نصب نمایید:

```bash
sudo pacman -S nvidia-open nvidia-utils nvidia-settings
```

> **نکته**
> اگر کرنل کاستوم یا کرنل lts نصب کرده‌اید باید درایور nvidia-open-dkms را نصب نمایید:
> ```bash
> sudo pacman -S nvidia-open-dkms nvidia-utils nvidia-settings
> ```
{.is-info}

> **هشدار**
> برای کارت‌های سری تورینگ، ممکن است درایور nvidia-open مشکلاتی در مدیریت انرژی RTD3 داشته باشد. در صورت بروز مشکل می‌توانید از درایور انحصاری استفاده کنید.
{.is-warning}

## فعال‌سازی DRM Kernel Mode Setting

از نسخه ۵۶۰.۳۵.۰۳-۵ به بعد، DRM به‌صورت پیش‌فرض فعال است. برای بررسی وضعیت آن:

```bash
cat /sys/module/nvidia_drm/parameters/modeset
```

اگر خروجی `Y` باشد، DRM فعال است.

> **نکته**
> از نسخه ۵۴۵ به بعد، پارامتر fbdev نیز اضافه شده که برای کنسول (tty) با رزولوشن بالا مفید است.
{.is-info}

برای فعال‌سازی دستی (در درایورهای قدیمی‌تر):

```bash
sudo tee /etc/modprobe.d/nvidia-modeset.conf <<< 'options nvidia_drm modeset=1 fbdev=1'
```

### بارگذاری زودهنگام ماژول‌ها

کاربران mkinitcpio نسخه ۴۰ به بالا نیازی به regenerate کردن دستی initramfs ندارند. برای نسخه‌های قدیمی‌تر، پس از اضافه کردن ماژول‌ها به MODULES، دستور زیر را اجرا کنید:

```bash
sudo mkinitcpio -P
```

## نکات مهم

### ۱. اجرای بازی‌ها با گرافیک انویدیا

برای اجرای بازی‌ها باید درایور ۳۲ بیتی انویدیا و mesa و ولکان هر دو نسخه ۶۴ و ۳۲ بیتی را نصب کنید.

اگر درایور انحصاری انویدیا یا nvidia-open را دارید:

```bash
sudo pacman -S vulkan-icd-loader lib32-vulkan-icd-loader lib32-nvidia-utils mesa lib32-mesa
```

اگر درایور nouveau دارید:

```bash
sudo pacman -S vulkan-icd-loader lib32-vulkan-icd-loader vulkan-nouveau lib32-vulkan-nouveau
```

### ۲. تنظیمات ویلند (Wayland)

> **توجه**
> از نسخه ۵۵۵ به بعد، پشتیبانی Explicit Sync اضافه شده که مشکلات flickering و تاخیر را در ویلند حل می‌کند.
{.is-info}

برای عملکرد بهتر ویلند، پارامترهای modeset و fbdev باید فعال باشند (که از نسخه ۵۶۰ به بعد به‌صورت پیش‌فرض فعال هستند).

برای بررسی fbdev:

```bash
cat /sys/module/nvidia_drm/parameters/fbdev
```

### ۳. مدیریت مصرف VRAM در ویلند

برخی کامپوزیتورهای ویلند ممکن است VRAM زیادی مصرف کنند. برای محدود کردن آن، فایل زیر را ایجاد کنید:

```bash
sudo mkdir -p /etc/nvidia/nvidia-application-profiles-rc.d/
sudo nano /etc/nvidia/nvidia-application-profiles-rc.d/50-limit-free-buffer-pool.json
```

محتوای فایل (برای مثال niri):

```json
{
    "rules": [
        {
            "pattern": {
                "feature": "procname",
                "matches": "niri"
            },
            "profile": "Limit free buffer pool on Wayland compositors"
        }
    ],
    "profiles": [
        {
            "name": "Limit free buffer pool on Wayland compositors",
            "settings": [
                {
                    "key": "GLVidHeapReuseRatio",
                    "value": 0
                }
            ]
        }
    ]
}
```

## سوییچ بین دو کارت گرافیک در لپ‌تاپ

برای این‌کار دو برنامه آسان و راحت وجود دارد:

### Bumblebee (توصیه نمی‌شود)

این برنامه به کمک فناوری NVIDIA Optimus موجود در گرافیک‌های انویدیا، بین دو گرافیک موجود با توجه به سنگینی کار در حال انجام، سوییچ می‌کند.

> **هشدار**
> بامبل‌بی قدیمی است و ممکن است با درایورهای جدید مشکل داشته باشد. از Envycontrol استفاده کنید.
>{.is-warning}

برای نصب آن به این شکل عمل کنید:

```bash
sudo pacman -S bumblebee mesa lib32-nvidia-utils lib32-virtualgl
```

سپس کاربر خود را به گروه بامبل‌بی اضافه نموده و سپس سرویس بامبل‌بی را روشن کنید (منظور از $USER نام یوزر شماست):

```bash
sudo gpasswd -a $USER bumblebee && sudo systemctl enable --now bumblebeed.service
```

در نهایت سیستم خود را ریستارت کنید.

#### مدیریت انرژی در بامبل‌بی

بامبل‌بی به صورت خودکار کارت گرافیک مجزا را در هنگام بیکاری، خاموش نمی‌کند بنابراین ما نیازمند برنامه دیگری هستیم که این کار را انجام دهد، برنامه bbswitch این‌کار را برای ما انجام می‌دهد کافی است که آن را نصب کنیم:

```bash
sudo pacman -S bbswitch
```

برای کرنل lts یا کرنل‌های کاستوم:

```bash
sudo pacman -S bbswitch-dkms
```

### Envycontrol (توصیه می‌شود)

این برنامه همانند بامبل‌بی به کمک تکنولوژی NVIDIA Optimus کار می‌کند، اما برخلاف بامبل‌بی ۳ حالت مختلف دارد و کاربر باید آن را به صورت دستی تنظیم کند.

دستور نصب آن به این شکل است:

```bash
sudo pacman -S envycontrol
```

#### تنظیم حالت سوییچر envycontrol

**حالت هایبرید (Hybrid):** سیستم به صورت خودکار بین دو گرافیک سوییچ می‌کند:

```bash
sudo envycontrol -s hybrid
```

> **نکته**
> envycontrol برای کنترل مصرف انرژی در پردازنده‌های گرافیکی سری تورینگ به بالا انویدیا، فلگ `--rtd3` را دارد که مقدار پیش‌فرض آن ۲ است، ۱ کمترین درجه و ۳ بیشترین درجه آن است.
> 
> برای تنظیم آن به عنوان مثال:
> ```bash
> sudo envycontrol -s hybrid --rtd3 3
> ```
> 
> اگر پردازنده گرافیکتان سری پاسکال یا قدیمی‌تر است، از bbswitch استفاده کنید.
>{.is-info}

**استفاده فقط از گرافیک انویدیا:**

```bash
sudo envycontrol -s nvidia --dm sddm
```

**استفاده فقط از گرافیک مجتمع (Intel/AMD):**

```bash
sudo envycontrol -s integrated --dm sddm
```

(منظور از `--dm` دیسپلی منیجر توزیعتان است مانند sddm یا gdm)
