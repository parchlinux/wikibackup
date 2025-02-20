---
title: IDEها در پارچ
description: معرفی و آموزش نصب IDEهای محبوب در پارچ لینوکس
published: true
date: 2025-02-13T07:53:24.094Z
tags: ide, ides, vscode, code, editor, development, programing, برنامه‌نویسی, ادیتور, کد
editor: markdown
dateCreated: 2025-02-07T18:55:15.321Z
---

# ابزارهای توسعه نرم‌افزار (IDE)

## درباره
ابزارهای توسعه نرم‌افزار (Integrated Development Environment - IDE) محیط‌هایی هستند که شامل ویرایشگر متن، مدیریت پروژه، دیباگر(Debuger) و ابزارهای دیگر برای توسعه نرم‌افزار می‌باشند.



## IDE‌های محبوب

### 1. **Visual Studio Code**
Visual Studio Code (VS Code) یکی از محبوب‌ترین و پرکاربرترین ویرایشگرهای کد است که توسط Microsoft توسعه داده شده.

#### نسخه‌های موجود:
- **Code - OSS**: بسته منبع‌باز رسمی آرچ لینوکس. این نسخه یک پیکربندی برای فعال‌سازی [Open VSX](https://open-vsx.org/) دارد. 
نصب:
```bash
sudo pacman -S code
```
  
- **Visual Studio Code**: نسخه اختصاصی و مالکیتی مایکروسافت.  
نصب:
```bash
paru -S visual-studio-code-bin
```

- **VSCodium**: نسخه آزاد جامعه که داده‌های مربوط به رفتار نرم‌افزار را به سرویس‌دهندگان ارسال نمی‌کند و پیکربندی [Open VSX](https://open-vsx.org/) را فراهم می‌کند.  
**نصب:**
```bash
paru -S vscodium
```

### 2. **JetBrains IntelliJ IDEA**
IntelliJ IDEA یک IDE حرفه‌ای برای توسعه نرم‌افزارهای Java است. این ابزار دارای ویژگی‌های قدرتمندی برای توسعه کد، مدیریت پروژه و تست است.
**نصب:**
```bash
sudo pacman -S intellij-idea-community-edition
```

### 3. **Eclipse**
Eclipse یک IDE آزاد برای توسعه نرم‌افزارهای Java است که از زبان های متنوعی پشتیبانی میکند. 
**نصب:**
```bash
sudo pacman -S eclipse-java-bin
```

### 4. **PyCharm**
PyCharm یک IDE اختصاصی برای زبان برنامه‌نویسی Python است که توسط JetBrains توسعه یافته است.
**نصب:**
```bash
sudo pacman -S pycharm-community-edition
```

### 5. Zed
Zed یک ویرایشگر کد جدید است که با زبان برنامه‌نویسی Rust ساخته شده و بر سرعت، همکاری و هوش مصنوعی (AI) تمرکز دارد و از زبان های مختلف پشتیبانی میکند.
**نصب:**
```bash
sudo pacman -S zed
```

### 6. Atom/Pulsar
Pulsar یک ویرایشگر متن منبع‌باز است Pulsar یک ویرایشگر متن آزاد است که پس از توقف رسمی توسعه Atom توسط GitHub، توسط جامعه توسعه دهندگان توسعه یافته و به طور خاص برای تجربه‌ای سبک و قابل شخصی‌سازی طراحی شده است.
**نصب:**
```bash
paru -S pulsar
```

### 7. NetBeans
NetBeans یک IDE آزاد و قدرتمند است که توسط Oracle توسعه داده شده و به طور اصلی برای توسعه نرم‌افزارهای Java طراحی شده است. این ابزار از زبان‌های برنامه‌نویسی دیگر نیز پشتیبانی می‌کند
**نصب:**
```bash
sudo pacman -S netbeans
```

### 8. **All JetBrains products**
جعبه ابزار جتبرینز یک نرم‌افزار مدیریتی است که به شما امکان می‌دهد تا IDE‌های مختلف جتبرینز مانند IntelliJ IDEA، PyCharm، WebStorm و... را به راحتی نصب و مدیریت کنید. این ابزار از ویژگی‌هایی مانند بروزرسانی خودکار و جابه‌جایی بین نسخه‌های مختلف پشتیبانی می‌کند.
**نصب:**
```bash
sudo pacman -S jetbrains-toolbox
```

### 8. Vim/NeoVim
NeoVim به تنهایی یک IDE کامل نیست، اما با به‌کارگیری افزونه‌های فراوانی که برای آن توسعه یافته می‌توان آن را به یک محیط توسعه مشابه IDE تبدیل کرد.
> برای جزئیات بیشتر درباره NeoVim و چگونگی تبدیل آن به یک IDE کامل، می‌توانید به [صفحه مربوط به Neovim در ویکی پارچ](https://wiki.parchlinux.com/fa/neovim) مراجعه کنید.
{.is-info}
