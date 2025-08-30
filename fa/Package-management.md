---
title: مدیریت بسته
description: 
published: true
date: 2025-08-30T15:35:59.034Z
tags: 
editor: markdown
dateCreated: 2024-05-07T16:45:46.483Z
---

# مدیریت بسته در پارچ لینوکس


## ویدئو آموزشی کار با پک‌من و paru

شما می‌توانید بجای مطالعه تمام این مطالب ویدئو زیر را برای یادگیری کار با pacman و paru تماشا کنید.

<div style="position: relative; padding-top: 56.25%;"><iframe title="آموزش استفاده از pacman و paru در پارچ" width="100%" height="100%" src="https://tubedu.org/videos/embed/jz4hXemh7RFUp6HYgi6egK" frameborder="0" allowfullscreen="" sandbox="allow-same-origin allow-scripts allow-popups allow-forms" style="position: absolute; inset: 0px;"></iframe></div>

## مدیر بسته

مدیر بسته در پارچ لینوکس با نام pacman شناخته می‌شود.

طبق ویکی ArchLinux:

> مدیر بسته pacman یکی از ویژگی‌های ممتاز آرچ لینوکس است. این مدیر بسته فرمت ساده‌ای از بسته‌های دودویی را با یک سیستم ساخت آسان ترکیب می‌کند. هدف از pacman، مدیریت آسان بسته‌هااست ،بگونه‌ای که بتوان به راحتی بسته‌ها را مدیریت کرد، و از مخازن رسمی یا غیر رسمی هستند.
> pacman با هماهنگ کردن فهرست بسته‌ها با سرور اصلی، سیستم را به‌روز نگه می‌دارد. این مدل سرور/کاربر همچنین به کاربر اجازه می‌دهد که بسته‌ها را با یک دستور ساده دانلود/نصب کند، همراه با تمامی وابستگی‌های مورد نیاز.
> pacman به زبان برنامه‌نویسی C نوشته شده است و از فرمت tar bsdtar(1) برای بسته‌بندی استفاده می‌کند.

## چگونگی کار pacman

اینجا یک کتابچه راهنمای کوچک است که به شما در استفاده از pacman کمک می‌کند:

### عملیات اساسی

| عمل | Arch | Red Hat/Fedora | Debian/Ubuntu | SLES/openSUSE | Gentoo |
|--------|------|-----------------|----------------|-----------------|--------|
| جستجو برای بسته(ها) | `pacman -Ss` | `dnf search` | `apt search` | `zypper search` یا `zypper se [-s]` | `emerge --search` (`-s`) یا `emerge --searchdesc` (`-S`) |
| نصب بسته(ها) با نام | `pacman -S` | `dnf install` | `apt install` | `zypper install` یا `zypper in` | `emerge` |
| گرفتن بسته‌های منبع و وابستگی‌های ساخت | `makepkg -s PKGBUILD` | `dnf builddep` | `apt build-dep` | `zypper source-install` (`zypper si`) یا `zypper install -d` | `emerge`، یا به صراحت `emerge --with-bdeps` |
| چاپ اهداف بدون انجام عملیات | `pacman --print` (یا `-p`) | `dnf --setopt=tsflags=test` | `apt --simulate` (یا `-s`، `--dry-run`، `--just-print`) | `zypper --dry-run` | `emerge --pretend` (`-p`) |
| تغییر تأییدات | `pacman --confirm` یا `pacman --noconfirm` | `dnf --assumeyes` (`-y`) یا `dnf --assumeno` | `apt --yes` (`-y`) | `zypper --non-interactive` (`-n`) یا `zypper --no-confirm` (`-y`) | `emerge --ask` (`-a`) |
| بازآوری مخزن بسته محلی | `pacman -Sy` | `dnf check-update` یا `dnf makecache` یا `dnf upgrade` | `apt update` | `zypper refresh` یا `zypper ref` `[-s]` | `emerge --sync` |
| ارتقاء بسته‌ها | `pacman -Syu` | `dnf upgrade` | `apt upgrade` | `zypper update` یا `zypper up` | `emerge -[a]uDN @world` |
| ارتقاء بسته‌ها (ارتقاء‌های پیچیده) | `pacman -Syu` | `dnf distro-sync` | `apt dist-upgrade` | `zypper dup` | `emerge -[a]uDN @world` |
| حذف بسته(ها) و وابستگی‌ها | `pacman -Rs` | `dnf remove` | `apt autoremove` | `zypper remove` یا `zypper rm` | `emerge --depclean` (`-c`) |
| حذف بسته(ها) و فایل‌های پیکربندی | `pacman -Rn` | ? | `apt purge` | ? | n/a |
| حذف بسته(ها)، وابستگی‌ها و فایل‌های پیکربندی | `pacman -Rns` | ? | `apt autoremove --purge` | ? | n/a |
| حذف وابستگی‌های نیازمند | `pacman -Qdtq | pacman -Rs -` `` (`-Qdttq` for optional deps)| `dnf autoremove` | `apt autoremove` | `zypper rm -u` یا `zypper packages --unneeded` | `emerge --depclean` (`-c`) |
| حذف بسته‌هایی که در مخازن نیستند | ```pacman -Rs $(pacman -Qmq)```  | `dnf repoquery --extras` | `aptitude purge '~o'` || ? |
| نشان دادن بسته نصب شده به صورت صریح | `pacman -D --asexplicit` | `dnf mark install` | `apt-mark manual` | `zypper install --force` | `emerge --select` (`-w`) |
| نصب بسته(ها) به عنوان وابستگی | `pacman -S --asdeps` | `dnf install` سپس `dnf mark remove` | `apt-mark auto` | n/a ([راه حل](https://bugzilla.opensuse.org/show_bug.cgi?id=1175678)) | `emerge --oneshot` (`-1`) |
| فقط دانلود بسته(ها) | `pacman -Sw` | `dnf download` | `apt install --download-only` یا `apt download` | `zypper --download-only` | `emerge --fetchonly` (`-f`) |
| پاکسازی حافظه‌های محلی | `pacman -Sc` یا `pacman -Scc` | `dnf clean all` | `apt autoclean` یا `apt clean` | `zypper clean` | `eclean distfiles` |
| شروع یک پوسته | | `dnf shell` | | `zypper shell` ||

### استعلام بسته‌های خاص

| عمل | Arch | Red Hat/Fedora | Debian/Ubuntu | SLES/openSUSE | Gentoo |
|--------|------|-----------------|----------------|-----------------|--------|
| نمایش اطلاعات بسته | `pacman -Si` یا `pacman -Qi` | `dnf list` یا `dnf info` | `apt show` یا `apt-cache policy` | `zypper info` یا `zypper if` | `emerge -S`، `emerge -pv` یا `eix` |
| نمایش اطلاعات بسته محلی | `pacman -Qi` | `rpm -qi` / `dnf info installed` | `dpkg -s` یا `aptitude show` | `zypper --no-remote info` یا `rpm -qi` | `emerge -pv` یا `emerge -S` |
| نمایش اطلاعات بسته از راه دور | `pacman -Si` | `dnf info` | `apt-cache show` یا `aptitude show` | `zypper info` | `emerge -pv` و `emerge -S` یا `equery meta` |
| نمایش فایل‌های بسته محلی | `pacman -Ql` | `rpm -ql` | `dpkg -L` | `rpm -ql` | `equery files` یا `qlist` |
| نمایش فایل‌های بسته از راه دور | `pacman -Fl` | `dnf repoquery -l` یا `repoquery -l` | `apt-file list` || `pfl` |
| استعلام بسته‌ای که فایل را فراهم می‌کند | `pacman -Qo` | `rpm -qf` (نصب شده) یا `dnf provides` (همه) یا `repoquery -f` | `dpkg -S` یا `dlocate` | `rpm -qf` (نصب شده) یا `zypper search -f` (همه) | `equery belongs` یا `qfile` |
| لیست فایل‌ها در بسته | `pacman -Ql` یا `pacman -Fl` | `dnf repoquery -l` | `dpkg-query -L` | `rpm -ql` | `equery files` یا `qlist` |
| نمایش فراهم کننده‌های معکوس | `pacman -F` | `dnf provides` | `apt-file search` | `zypper what-provides` یا `zypper wp` (دقیق)

 یا `zypper se --provides` (مبهم) | `equery belongs` (نصب شده) یا `pfl` |
| جستجو بسته با فایل | `pacman -F` | `dnf provides` | `apt-file search` یا `auto-apt` | `zypper search -f` | `equery belongs` یا `qfile` |
| نمایش تغییرات بسته | `pacman -Qc` | `dnf changelog` | `apt-get changelog` | `rpm -q --changelog` | `equery changes -f` |

### AUR

> مخزن کاربران Arch (AUR) یک مخزن برای کاربران Arch است که توسط جامعه پشتیبانی می‌شود. این مخزن شامل توضیحات بسته‌ها (PKGBUILDs) است که به شما اجازه می‌دهد یک بسته را از منبع با makepkg کامپایل کرده و سپس آن را از طریق pacman نصب کنید. AUR برای سازماندهی و به اشتراک گذاری بسته‌های جدید از جامعه ایجاد شده است و برای کمک به اضافه کردن بسته‌های محبوب به مخزن اضافی، بروز شدن پکیج‌های معروف را تسریع می‌کند.
تعداد زیادی از بسته‌های جدیدی که وارد مخازن رسمی می‌شوند ابتدا در AUR شروع می‌شوند. در AUR، کاربران قادر به ارسال ساخت‌های بسته خود (PKGBUILD و فایل‌های مرتبط) هستند. جامعه AUR قادر به رای‌گیری برای بسته‌ها در AUR است. اگر یک بسته به اندازه کافی محبوب شود - تهیه شده با مجوز سازگار و تکنیک بسته‌بندی خوب - ممکن است به مخزن اضافی وارد شود (که مستقیماً توسط pacman یا از طریق سیستم ساخت Arch قابل دسترس است).

### مدیر AUR

پارچ لینوکس، paru را به عنوان مدیر AUR دارد.
استفاده از paru مانند استفاده از pacman است، با همان نحوه‌ی نوشتاری می‌توانید به‌راحتی بسته‌ها را از AUR نصب کنید.
در هنگام استفاده از paru، نیازی به اجرای آن با sudo نیست، زیرا در صورت نیاز، خود ابزار دسترسی ریشه را درخواست می‌کند.
#### استفاده از Paru
در زیر چند دستور paru مفید آمده است:

| دستور | توضیحات |
| --- | --- |
| `paru` | بروزرسانی کامل سیستم |
| `paru -Syu` | بروزرسانی کامل سیستم |
| `paru -S نام‌برنامه` | نصب برنامه از AUR |
| `paru نام‌برنامه` | نصب برنامه از AUR، با انتخاب از لیست |
| `paru -Sc` | پاک کردن حافظه‌های پنهان Pacman و Paru |
| `paru -Ss نام‌برنامه` | جستجو برای یک بسته |
