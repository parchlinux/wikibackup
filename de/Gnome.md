---
title: GNOME-Desktopumgebung
description: 
published: true
date: 2024-10-17T09:39:30.505Z
tags: gnome
editor: markdown
dateCreated: 2024-10-17T09:39:27.243Z
---

# Was ist GNOME?
> GNOME (/(ɡ)noʊm/) ist eine Desktopumgebung, die einfach und benutzerfreundlich sein soll. Sie wurde vom GNOME-Projekt entwickelt und besteht vollständig aus freier Open-Source-Software.


### Screenshot von Gnome in Parch Linux

![screenshot](https://github.com/parchlinux/Parch-iso-gnome/raw/main/image/screenshot.png)

## Von einem anderen Desktop zu Gnome wechseln

Um Gnome auf Parch Linux zu installieren, müssen Sie unser Metapaket installieren.

```bash
sudo pacman -S parch-gnome-meta
```
Dadurch würde eine minimale Gnome-Sitzung mit Parch-Anpassung auf Parch Linux installiert.

### Aktivieren des Display-Managers
Wenn Sie von KDE oder anderen Desktops wechseln (standardmäßig verwendet Parch SDDM in allen Editionen außer Gnome), müssen Sie Ihren alten Login-Manager deaktivieren und dann GDM aktivieren.

```bash
# Deaktivieren des alten Login-Managers (sddm)
sudo systemctl disable sddm

# Aktivieren GDM
sudo systemctl enable gdm
```


## Tips und Tricks

### Numlock beim GNOME-Start aktivieren

Sie müssen diesen Befehl im Terminal ausführen, um dieses Verhalten zu aktivieren:
```bash
gsettings set org.gnome.desktop.peripherals.keyboard numlock-state true
```

So merken Sie sich den letzten Zustand:
```bash
gsettings set org.gnome.desktop.peripherals.keyboard remember-numlock-state true
```


### Bestimmte URLs auf bestimmte Webbrowser umleiten

Dies zeigt, wie Chromium für bestimmte URL-Typen verwendet wird, während Firefox als Standardbrowser für alle anderen Aufgaben beibehalten wird.

Stellen Sie sicher, dass pcre installiert ist, um pcregrep zu verwenden.

Richten Sie benutzerdefiniertes xdg-open ein:
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

Konfigurieren Sie Domänen für die Weiterleitung zu Chromium:‍

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
Richten Sie xdg-open web als Desktopanwendung ein:
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
Legen Sie xdg-open web als Standard-Webanwendung in den GNOME-Einstellungen fest: Gehen Sie zu GNOME-Einstellungen > Details > Standardanwendungen und legen Sie Web auf xdg-open web fest.


### Benutzerdefinierte GNOME-Sitzungen
Es ist möglich, benutzerdefinierte GNOME-Sitzungen zu erstellen, die den GNOME-Sitzungsmanager verwenden, aber unterschiedliche Komponentensätze starten (z. B. Openbox mit tint2 statt GNOME Shell).

Für eine benutzerdefinierte GNOME-Sitzung sind zwei Dateien erforderlich: eine Sitzungsdatei in ```/usr/share/gnome-session/sessions/``` der die zu startenden Komponenten definiert und einen Desktop-Eintrag in `/usr/share/xsessions` die vom Display-Manager gelesen wird. Nachfolgend finden Sie eine Beispiel-Sitzungsdatei:
```
/usr/share/gnome-session/sessions/gnome-openbox.session
```
```
[GNOME Session]
Name=GNOME Openbox
RequiredComponents=openbox;tint2;gnome-settings-daemon;
```
Und eine Beispiel-Desktopdatei:
```
/usr/share/xsessions/gnome-openbox.desktop
```
```
[Desktop Entry]
Name=GNOME Openbox
Exec=gnome-session --session=gnome-openbox
```



