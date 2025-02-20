---
title: Paketverwaltung
description: 
published: true
date: 2024-05-31T16:52:02.409Z
tags: 
editor: markdown
dateCreated: 2024-05-31T16:51:56.222Z
---

# Paketverwaltung in Parch Linux

## Paketverwaltung

Der Paketmanager in Parch Linux heißt Pacman.

Laut dem ArchLinux-Wiki:

>Der Paketmanager Pacman ist eines der wichtigsten Unterscheidungsmerkmale von Arch Linux. Er kombiniert ein einfaches binäres Paketformat mit einem benutzerfreundlichen Build-System. Das Ziel von Pacman ist es, die einfache Verwaltung von Paketen zu ermöglichen, egal ob sie aus den offiziellen Repositories oder den eigenen Builds des Benutzers stammen. 
Pacman hält das System auf dem neuesten Stand, indem es Paketlisten mit dem Masterserver synchronisiert. Dieses Server/Client-Modell ermöglicht es dem Benutzer auch, Pakete mit einem einfachen Befehl herunterzuladen/zu installieren, komplett mit allen erforderlichen Abhängigkeiten. 
Pacman ist in der Programmiersprache C geschrieben und verwendet das Tar-Format bsdtar(1) zum Verpacken.


## Wie funktioniert Pacman?

Hier ist ein kleiner Spickzettel, der Ihnen bei der Verwendung von Pacman hilft:

## Grundoperationen

| Aktion | Arch | Red Hat/Fedora | Debian/Ubuntu | SLES/openSUSE | Gentoo |
|--------|------|-----------------|----------------|-----------------|--------|
| Nach Paket(en) suchen | `pacman -Ss` | `dnf search` | `apt search` | `zypper search` oder `zypper se [-s]` | `emerge --search` (`-s`) oder `emerge --searchdesc` (`-S`) |
| Pakete nach Namen installieren | `pacman -S` | `dnf install` | `apt install` | `zypper install` oder `zypper in` | `emerge` |
| Quellpaket(e) abrufen und Abhängigkeiten erstellen | `makepkg -s PKGBUILD` | `dnf builddep` | `apt build-dep` | `zypper source-install` (`zypper si`) oder `zypper install -d` | `emerge`, oder ausdrücklich `emerge --with-bdeps` |
| Ziele drucken, ohne den Vorgang auszuführen | `pacman --print` (oder `-p`) | `dnf --setopt=tsflags=test` | `apt --simulate` (oder `-s`, `--dry-run`, `--just-print`) | `zypper --dry-run` | `emerge --pretend` (`-p`) |
| Bestätigungen umschalten | `pacman --confirm` oder `pacman --noconfirm` | `dnf --assumeyes` (`-y`) oder `dnf --assumeno` | `apt --yes` (`-y`) | `zypper --non-interactive` (`-n`) oder `zypper --no-confirm` (`-y`) | `emerge --ask` (`-a`) |
| Lokales Paket-Repository aktualisieren | `pacman -Sy` | `dnf check-update` oder `dnf makecache` oder `dnf upgrade` | `apt update` | `zypper refresh` oder `zypper ref` `[-s]` | `emerge --sync` |
| Upgrade-Pakete | `pacman -Syu` | `dnf upgrade` | `apt upgrade` | `zypper update` oder `zypper up` | `emerge -[a]uDN @world` |
| Upgrade-Pakete (komplexe Updates) | `pacman -Syu` | `dnf distro-sync` | `apt dist-upgrade` | `zypper dup` | `emerge -[a]uDN @world` |
| Entfernen Sie ein oder mehrere Pakete und Abhängigkeiten | `pacman -Rs` | `dnf remove` | `apt autoremove` | `zypper remove` or `zypper rm` | `emerge --depclean` (`-c`) |
| Pakete und Konfigurationsdateien entfernen | `pacman -Rn` | ? | `apt purge` | ? | n/a |
| Entfernen Sie Pakete, Abhängigkeiten und Konfigurationsdateien | `pacman -Rns` | ? | `apt autoremove --purge` | ? | n/a |
| Entfernen Sie nicht benötigte Abhängigkeiten | `pacman -Qdtq | pacman -Rs -` `` (`-Qdttq` für optionale Abhängigkeiten)| `dnf autoremove` | `apt autoremove` | `zypper rm -u` or `zypper packages --unneeded` | `emerge --depclean` (`-c`) |
| Entfernen Sie Pakete, die sich nicht in Repositories befinden | ```pacman -Rs $(pacman -Qmq)```  | `dnf repoquery --extras` | `aptitude purge '~o'` || ? |
| Installiertes Paket als ausdrücklich erforderlich markieren | `pacman -D --asexplicit` | `dnf mark install` | `apt-mark manual` | `zypper install --force` | `emerge --select` (`-w`) |
| Paket(e) als Abhängigkeit installieren | `pacman -S --asdeps` | `dnf install` dann `dnf mark remove` | `apt-mark auto` | n/a ([workaround](https://bugzilla.opensuse.org/show_bug.cgi?id=1175678)) | `emerge --oneshot` (`-1`) |
| Nur Paket(e) herunterladen | `pacman -Sw` | `dnf download` | `apt install --download-only` oder `apt download` | `zypper --download-only` | `emerge --fetchonly` (`-f`) |
| Lokale Caches bereinigen | `pacman -Sc` oder `pacman -Scc` | `dnf clean all` | `apt autoclean` oder `apt clean` | `zypper clean` | `eclean distfiles` |
| Starten einer Shell | | `dnf shell` | | `zypper shell` ||

## Abfragen bestimmter Pakete

| Aktion | Arch | Red Hat/Fedora | Debian/Ubuntu | SLES/openSUSE | Gentoo |
|--------|------|-----------------|----------------|-----------------|--------|
| Paketinformationen anzeigen | `pacman -Si` oder `pacman -Qi` | `dnf list` oder `dnf info` | `apt show` oder `apt-cache policy` | `zypper info` oder `zypper if` | `emerge -S`, `emerge -pv` oder `eix` |
| Lokale Paketinformationen anzeigen | `pacman -Qi` | `rpm -qi` / `dnf info installed` | `dpkg -s` oder `aptitude show` | `zypper --no-remote info` oder `rpm -qi` | `emerge -pv` oder `emerge -S` |
| Remote-Paketinformationen anzeigen | `pacman -Si` | `dnf info` | `apt-cache show` oder `aptitude show` | `zypper info` | `emerge -pv` and `emerge -S` oder `equery meta` |
| Lokale Paketdateien anzeigen | `pacman -Ql` | `rpm -ql` | `dpkg -L` | `rpm -ql` | `equery files` oder `qlist` |
| Remote-Paketdateien anzeigen | `pacman -Fl` | `dnf repoquery -l` oder `repoquery -l` | `apt-file list` || `pfl` |
| Abfragepaket, das Datei bereitstellt | `pacman -Qo` | `rpm -qf` (installed) oder `dnf provides` (alles) oder `repoquery -f` | `dpkg -S` oder `dlocate` | `rpm -qf` (installed) oder `zypper search -f` (alles) | `equery belongs` oder `qfile` |
| Auflisten der Dateien im Paket | `pacman -Ql` oder `pacman -Fl` | `dnf repoquery -l` | `dpkg-query -L` | `rpm -ql` | `equery files` oder `qlist` |
| Umgekehrte Angebote anzeigen | `pacman -F` | `dnf provides` | `apt-file search` | `zypper what-provides` oder `zypper wp` (exact)

 oder `zypper se --provides` (fuzzy) | `equery belongs` (installed) or `pfl` |
| Paket nach Datei suchen | `pacman -F` | `dnf provides` | `apt-file search` oder `auto-apt` | `zypper search -f` | `equery belongs` oder `qfile` |
| Paket-Änderungsprotokoll anzeigen | `pacman -Qc` | `dnf changelog` | `apt-get changelog` | `rpm -q --changelog` | `equery changes -f` |



## AUR

> Das Arch User Repository (AUR) ist ein von der Community betriebenes Repository für Arch-Benutzer. Es enthält Paketbeschreibungen (PKGBUILDs), mit denen Sie ein Paket mit makepkg aus dem Quellcode kompilieren und dann über pacman installieren können. Das AUR wurde erstellt, um neue Pakete aus der Community zu organisieren und freizugeben und die Aufnahme beliebter Pakete in das zusätzliche Repository zu beschleunigen.
Eine große Anzahl neuer Pakete, die in die offiziellen Repositories aufgenommen werden, beginnen im AUR. Im AUR können Benutzer ihre eigenen Paket-Builds (PKGBUILD und zugehörige Dateien) beitragen. Die AUR-Community kann für Pakete im AUR stimmen. Wenn ein Paket populär genug wird – vorausgesetzt, es verfügt über eine kompatible Lizenz und eine gute Verpackungstechnik – kann es in das zusätzliche Repository aufgenommen werden (direkt zugänglich über pacman oder vom Arch-Build-System aus). 


### AUR Manager

Parch Linux hat Paru, ebenso wie AUR Manager.
Die Verwendung von Paru ist genau wie die Verwendung von Pacman; mit der gleichen Syntax können Sie problemlos Pakete von AUR installieren.

#### Paru verwenden
Hier sind einige nützliche Paru-Befehle:

| Befehl | Beschreibung |
| --- | --- |
| `paru` | Aktualisieren Sie das gesamte System |
| `paru -Syu` | Aktualisieren Sie das gesamte System |
| `paru -S appname` | Installieren Sie das Programm von AUR |
| `paru appname` | Installieren Sie das Programm von AUR und wählen Sie aus der Liste |
| `paru -Sc` | Pacman- und Paru-Caches entfernen |
| `paru -Ss appname` | Nach einem Paket suchen |

