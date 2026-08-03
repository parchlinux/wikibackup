---
title: پارچ ریسک پنج
description: ریسک پنج یک معماری جایگزین و آزاد برای معماری‌های اینتلی و آرم می‌باشد.
published: true
date: 2025-02-08T16:03:48.007Z
tags: 
editor: markdown
dateCreated: 2025-02-08T16:02:39.332Z
---

# پارچ ریسک پنج

## ریسک پنج چیست؟
RISC-V (تلفظ: ریسک-فایو) یک معماری مجموعه دستورالعمل (ISA) بازمتن (Open-Source) و مبتنی بر فلسفه پردازش کاهش‌یافته دستورالعمل (RISC) است. این معماری به عنوان یک استاندارد آزاد و بدون محدودیت‌های حق امتیاز طراحی شده و انقلابی در دنیای سختافزارهای کامپیوتری محسوب می‌شود.

## پارچ بر روی ریسک پنج

این فقط برای تست Parch Gnu/Linux بر روی RISC-V است.



### پیش‌نیازها

- `arch-install-scripts`
- `parted`
- `git`
- `qemu-img`
- `qemu-system-riscv`
- `riscv64-linux-gnu-gcc`
- `devtools-riscv64`

همه پیش‌نیازها در مخزن موجود هستند و می‌توانید با استفاده از دستور زیر آن‌ها را نصب کنید:

```bash
sudo pacman -S arch-install-scripts parted git qemu-img devtools-riscv64 qemu-system-riscv riscv64-linux-gnu-gcc
```


### مراحل ساخت
مخزن پارچ ریسک پنج را کلون کنید:
```bash
git clone --depth 1 https://git.parchlinux.com/ports/parch-riscv.git
```
سپس برای ساخت RootFS و تصویر Qcow، از دستورات زیر استفاده کنید:

```bash
‎./mkrootfs
‎./mkimg
```

### شروع QEMU

>شما ابتدا باید از initrd fallback استفاده کنید و سپس با استفاده از دستور `mkinitcpio -P` initramfs را دوباره تولید کنید تا بتوانید از نسخه غیر fallback استفاده کنید. 
{.is-warning}


برای شروع QEMU، از دستور زیر استفاده کنید:

```bash
‎./startqemu.sh [qcow Image]
```

برای تست این سیستم، به Parch Linux نیاز دارید.