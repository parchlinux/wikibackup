---
title: Distrobox
description: 
published: true
date: 2025-05-08T12:41:35.400Z
tags: distrobox, podman, docker
editor: markdown
dateCreated: 2025-05-08T12:41:35.400Z
---

# Distrobox	
> Distrobox ist eine Container-Wrapper-Schicht, die es dem Benutzer ermöglicht, containerisierte Versionen von Linux zu installieren, die sich vom Host-System unterscheiden, während sie eine enge Integration mit dem Host bietet und die Ausführung von Binärdateien ermöglicht, die für eine Distribution entwickelt wurden, auf einer anderen.



Distrobox selbst ist kein Container-Manager und verlässt sich auf Podman oder [Docker](https://wiki.parchlinux.com/de/docker), um Container zu erstellen.

Aus der Distrobox Dokumentation:

> Verwenden Sie jede beliebige Linux-Distribution innerhalb Ihres Terminals. Aktivieren Sie sowohl Rückwärts- als auch Vorwärtskompatibilität mit Software und nutzen Sie die Freiheit, die Distribution zu verwenden, mit der Sie sich am wohlsten fühlen. Distrobox verwendet Podman oder Docker, um Container zu erstellen, basierend auf der Linux-Distribution Ihrer Wahl. Der erstellte Container wird eng mit dem Host-System integriert sein und das Teilen des HOME-Verzeichnisses des Benutzers, externen Speichers, externer USB-Geräte und grafischer Anwendungen (X11/Wayland) sowie die Audiowiedergabe ermöglichen.

## Sicherheitsauswirkungen

Das Hauptziel von Distrobox ist nicht darauf ausgerichtet, die Container vom Host-System zu isolieren, und die Container, die innerhalb von Distrobox laufen, würden vollen Zugriff auf dein Heimatverzeichnis sowie einige andere Orte haben.

Es wird empfohlen, **Podman** anstelle von **Docker** zu verwenden, da Docker standardmäßig Container als Root ausführt und root-basierte Container **uneingeschränkten Zugriff auf das Host-Dateisystem haben werden.**


## Installation

### Mit Root-Zugriff

Zuerst müssen Sie entweder Podman oder Docker installieren, um zu beginnen.

Installiere dann ```distrobox``` oder ```distrobox-git``` vom AUR mit paru.

### Ohne Root-Zugriff

Es ist möglich, Distrobox in deinen Heimatordner zu installieren, wenn du keinen Root-Zugriff auf das System hast oder wenn du eine unveränderliche Distro verwendest. Dazu ist die Verwendung eines curl-to-sh-Pipes erforderlich, was eine nicht unterstützte Installationsmethode ist, da dies ein Sicherheitsrisiko darstellt.

Sie finden Anweisungen auf der [Distrobox-Dokumentationsseite](https://distrobox.privatedns.org/#curl-or-wget)

## Verwendung
> Notiz:
> - Im folgenden Abschnitt ist ```name``` eine Variable und kann beliebig gewählt werden. Ersetzen Sie ```name``` in allen Fällen durch den gewählten Namen.
> - Für die vollständige Liste der unterstützten Optionen in einer beliebigen Unterkategorie verwenden Sie ```--help```. Beispielsweise um alle Erstellungsoptionen anzuzeigen, verwenden Sie ```distrobox create --help```.
> - Eine vollständige Liste der unterstützten Distros zusammen mit ihren Imagename finden Sie unter https://distrobox.it/compatibility/#containers-distros.
> - Für weiterführende Nutzungstechniken besuchen Sie bitte die Distrobox-Dokumentationsseite unter https://distrobox.it/usage/usage/


Um einen neuen Container zu erstellen, führen Sie den folgenden Befehl aus:
```bash
distrobox create -n name
```

Liste der installierten Container:
```bash
distrobox list
```

Um mit einem installierten Container zu interagieren: 
```bash
distrobox enter name
```

oder Sie können einen Befehl direkt ausführen:
```bash
distrobox enter name -- command
```

Um einen laufenden Container zu stoppen, führen Sie Folgendes aus:
```
distrobox stop name
```

Um einen Container zu löschen, führen Sie folgenden Befehl aus:
```
distrobox rm name
```



Um eine bestimmte Distro in einem Container zu installieren, führen Sie Folgendes aus (in diesem Beispiel ist es Ubuntu):
```
distrobox create --image ubuntu:22.04
```

Installationen können wie folgt vollständig angepasst werden (in diesem Beispiel ist es ein Container namens test, der Gentoo mit Root-Zugriff ausführt):
```
distrobox create -i docker.io/gentoo/stage3:latest -n test --root
```


Falls Sie benötigen, dass Ihr Container Root-Zugriff auf den Host hat, wird empfohlen, dass Sie das ```--root```-Flag anstelle von ```sudo distrobox``` verwenden.


## Configuration
It is possible to configure Distrobox in two ways, either with a configuration file or by using environment variables. 

### Konfigurationsdateien

Distrobox überprüft die folgenden Stellen auf Konfigurationsdateien, von der geringsten bis zur höchsten Priorität:

    /usr/share/distrobox/distrobox.conf
    /usr/etc/distrobox/distrobox.conf
    /etc/distrobox/distrobox.conf
    ~/.config/distrobox/distrobox.conf
    ~/.distroboxrc

Eine Beispiel-Konfigurationsdatei sieht wie folgt aus:

```
container_always_pull="1"
container_generate_entry=0
container_manager="docker"
container_image_default="registry.opensuse.org/opensuse/toolbox:latest"
container_name_default="test-name-1"
container_user_custom_home="$HOME/.local/share/container-home-test"
container_init_hook="~/.local/distrobox/a_custom_default_init_hook.sh"
container_pre_init_hook="~/a_custom_default_pre_init_hook.sh"
non_interactive="1"
skip_workdir="0"
```

### Environment variables

Die folgenden Variablen sind verfügbar und sollten mit Benutzervariablen gesetzt werden:

```
DBX_CONTAINER_ALWAYS_PULL
DBX_CONTAINER_CUSTOM_HOME
DBX_CONTAINER_IMAGE
DBX_CONTAINER_MANAGER
DBX_CONTAINER_NAME
DBX_CONTAINER_ENTRY
DBX_NON_INTERACTIVE
DBX_SKIP_WORKDIR
```

