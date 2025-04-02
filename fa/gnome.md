---
title: گنوم
description: 
published: true
date: 2025-04-02T19:53:41.215Z
tags: پارچ, گنوم
editor: markdown
dateCreated: 2024-11-20T15:39:31.166Z
---

# گنوم چیست؟
> گنوم (/(ɡ)noʊm/) یک محیط میزکار است که هدف سادگی و آسان بودن برای استفاده کردن است. It is designed by The GNOME Project and is composed entirely of free and open-source software.


### اسکرین‌شات از گنوم در پارچ لینوکس

![screenshot](https://github.com/parchlinux/Parch-iso-gnome/raw/main/image/screenshot.png)

## مهاجرت از میزکارهای دیگر به گنوم

برای نصب گنوم روی پارچ لینوکس، شما باید متاپکیچ ما را نصب کنید:

```bash
sudo pacman -S parch-gnome-meta
```
این یک نشست گنوم مینیمال با شخصی‌سازی پارچ، روی پارچ لینوکس نصب می‌کند. 

### فعال‌کردن مدیر نمایش
if you are moving from KDE or other desktops (به‌صورت پیش فرض پارچ در تمامی نسخه‌ها از sddm استفاده می‌کند به جز گنوم) you need to disable your old login manager and then enable GDM .

```bash
# disabling old login manager (sddm)
sudo systemctl disable sddm

#enabling GDM
sudo systemctl enable gdm
```


## نکات و ترفندها

### فعال‌سازی نامبرلاک در میزکار گنوم

برای فعال‌سازی این رفتار، این دستور را در ترمینال وارد کنید:
```bash
gsettings set org.gnome.desktop.peripherals.keyboard numlock-state true
```

برای اینکه گنوم، هربار فعال یا فعال نبودن را به خاطر بسپارد:
```bash
gsettings set org.gnome.desktop.peripherals.keyboard remember-numlock-state true
```


### هدایت پیوندهای خاص به مرورگرهای خاصی

This shows how to use Chromium for certain types of URLs while maintaining Firefox as default browser for all other tasks.

مطمئن شوید برای استفاده از `pcregrep` بسته `pcre` نصب شده است.

تنظیم xdg-open سفارشی:
```
/usr/local/bin/xdg-open
```
```
#!/bin/bash
DOMAIN_LIST_FILE=~/'domains.txt'
OTHER_BROWSER='/usr/bin/chromium-browser'
BROWSER_OPTIONS='' # Optional, for command line options passed to browser
XDG_OPEN='/usr/bin/xdg-open'
DEFAULT_BROWSER='/usr/bin/firefox'

if echo "$1" | pcregrep -q '^https?://'; then
    matching=0
    while read domain; do
	if echo "$1" | pcregrep -q "^https?://${domain}"; then
	    matching=1
	    break
	fi
    done < "$DOMAIN_LIST_FILE"

    if [[ $matching -eq 1 ]]; then
	"$OTHER_BROWSER" $BROWSER_OPTIONS ${*}
	exit 0
    fi
    
    "$DEFAULT_BROWSER" ${*}
    exit 0
else
    "$XDG_OPEN" ${*}
fi
```

کانفیگ کردن دامنه‌ها برای هدایت شدن به کرومیوم:

```
$HOME/domains.txt
```
```
stackexchange.com
stackoverflow.com
superuser.com
www.youtube.com
github.com
```
تنظیم xdg-open web به عنوان برنامه میزکار:
```
$HOME/.local/share/applications/xdg-open-web.desktop
```
```
[Desktop Entry]
Version=1.0
Name=xdg-open web
GenericName=Web Browser
Exec=xdg-open %u
Terminal=false
Type=Application
MimeType=text/html;text/xml;application/xhtml+xml;application/vnd.mozilla.xul+xml;text/mml;x-scheme-handler/http;x-scheme-handler/https;
StartupNotify=true
Categories=Network;WebBrowser;
Keywords=web;browser;internet;
Actions=new-window;new-private-window;
```
```
$ update-desktop-database $HOME/.local/share/applications/
```
Set xdg-open web as default Web application in GNOME settings: Go to GNOME Settings > Details > Default Applications and set Web to xdg-open web


### نشست های سفارشی گنوم
ایجاد نشست‌های سفارشی گنوم که از مدیر نشست گنوم استفاده می‌کنند اما مجموعه‌های مختلفی از اجزاء را شروع می‌کنند؛ ممکن است. (برای مثال `Openbox` با `tint2` به جای `GNOME Shell`).

Two files are required for a custom GNOME session: a session file in ```/usr/share/gnome-session/sessions/``` which defines the components to be started and a desktop entry in `/usr/share/xsessions` which is read by the display manager. یک نمونه فایل نشست در زیر ارائه داده شده است: 
```
/usr/share/gnome-session/sessions/gnome-openbox.session
```
```
[GNOME Session]
Name=GNOME Openbox
RequiredComponents=openbox;tint2;gnome-settings-daemon;
```
و یک نمونه فایل دسکتاپ: 
```
/usr/share/xsessions/gnome-openbox.desktop
```
```
[Desktop Entry]
Name=GNOME Openbox
Exec=gnome-session --session=gnome-openbox
```
