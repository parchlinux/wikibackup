---
title: Docker
description: 
published: true
date: 2025-04-17T14:06:05.656Z
tags: docker
editor: markdown
dateCreated: 2025-04-10T18:27:56.858Z
---

# Docker Übersicht
Docker ist ein Werkzeug für die Containerisierung, das das Teilen von Entwicklungsumgebungen über verschiedene Betriebssysteme hinweg ermöglicht. Diesbeschleunigt die Entwicklungzeit und ermöglicht es Teammitgliedern, Umgebungen ohne Abhängigkeitskonflikte zu teilen, da alle Abhängigkeiten in dem Container enthalten und isoliert sind.

# Geschichte
Bevor die Konzepte von Containern und Umgebungsisolierung entwickelt wurden, war die Virtualisierung die Hauptlösung, um Entwicklungsumgebungen vom Host-System zu trennen. Benutzer würden CPU-, Speicher- und Festplattenspeicherressourcen einem virtuellen System zuweisen, aber dieser Ansatz war nicht optimal, da ein erheblicher Teil der Ressourcen vom virtuellen Betriebssystem verbraucht wurde, was zu langsameren Verarbeitungsgeschwindigkeiten im Vergleich zum Host-System führte.

Mit dem Aufkommen von Containern wurde die Isolation und Trennung verschiedener Umgebungen kostengünstiger und ressourcenschonender. Docker ist eines der Tools, das für die Erstellung und Verwaltung von Containern verwendet werden kann. Wenn Sie Ihre Entwicklung-/Produktionsumgebung mit anderen teilen müssen, erleichtert Docker dies, indem es Ihnen ermöglicht, Ihre Container-Skelettdatei (Image) zu teilen, wodurch der Prozess beschleunigt wird. Zusätzlich müssen andere Benutzer sich keine Sorgen um die Auflösung von Abhängigkeiten machen, da diese bereits im Container enthalten sind.

# Installation und Setup
Die [Docker-Dokumentation](https://docs.docker.com/engine/install) bietet umfassende Installationsanweisungen für Linux-Systeme. Allerdings werden Distributionen, die auf Arch Linux basieren, nicht offiziell unterstützt und die Installation gilt als instabil.

1. Öffnen Sie Ihr Terminal und installieren Sie Docker mit dem Paketmanager:

   ```
   sudo pacman -S docker
   ```
   > Wenn Sie auf den Fehler "Docker Not Found" stoßen, sollten Sie Ihre Repositorys mit dem Befehl "sudo pacman -Syu" aktualisieren.

2. Wenn Sie SystemD als Init System verwenden, aktivieren Sie den Docker Service mit:

   ```
   sudo systemctl enable --now docker.service
   ```

3. Fügen Sie Ihren Benutzernamen der Docker Gruppe hinzu:

   ```
   sudo usermod -aG docker $USER
   ```
   > Um die Änderungen anzuwenden, melden Sie sich entweder ab und wieder an oder verwenden Sie den Befehl `newgrp docker`.

4. Überprüfen Sie die Docker-Installation, indem Sie das Hello-World Bild ausführen:

   ```
   docker run hello-world
   ```

Der `run`-Befehl führt Images aus, die Baupläne für Container sind, die aus vordefinierten Dateien und Konfigurationen bestehen.

Um die Bilder in Ihrem System aufzulisten, verwenden Sie `docker images`.

Verwenden Sie, um aktive Container aufzulisten, `docker ps`.

# Docker Hub

[Docker Hub](https://hub.docker.com/) dient als Standard -Repository von Docker zum Herunterladen und Hochladen von Bildern.

Zum Beispiel, wenn Sie nginx als Ihren Webserver verwenden möchten, können Sie das nginx-Image von Docker Hub herunterladen und daraus einen Container erstellen.

1. Melden Sie sich in Ihrem Docker Hub Konto an:

   ```
   docker login
   ```
   > Wenn Sie kein Konto haben, erstellen Sie ein [hier](https://app.docker.com/signup).

2. Laden Sie das neueste Nginx-Bild mit:

   ```
   docker pull nginx
   ```

   > Leider ist Docker Hub im Iran blockiert. Wenn Sie auf einen 403-Fehler oder eine Verbindungstimeout stoßen, liegt dies wahrscheinlich an diesen Einschränkungen. Verwenden Sie den [Sanctions-Workaround](#sanctions-workaround), um dieses Problem zu lösen.
   
   > Der nginx-Webserver hat [umfassende Dokumentation](https://wiki.parchlinux.com/fa/Docker) auf Docker Hub über die Arbeit mit Images und Containern.

Erstellen Sie nach dem Herunterladen des Bildes einen Container für Nginx mit:

```
docker run --name some-nginx -p 8080:80 -v /some/content:/usr/share/nginx/html:ro -d nginx
```

> Wenn Sie andere Spiegel wie focker.ir verwenden, um Bilder herunterzuladen, ersetzen Sie `nginx` durch `focker.ir/nginx`.

```
docker run --name some-nginx -p 8080:80 -v /some/content:/usr/share/nginx/html:ro -d focker.ir/nginx
```

1. Die `--name` Option weist dem Container einen Namen zu, in diesem Beispiel `some-nginx`.
2. Die `-v` oder `--volume` Flag teilt einen (Pfad im Hostsystem) mit (einem Pfad im Container).

   > Im diesem Beispiel wird der Pfad `/some/content` im Host-System mit `/usr/share/nginx/html` im Container gemeinsam genutzt. Wenn Sie beispielsweise eine Datei mit dem Namen `name.txt` im Pfad `/some/content` im Host-System erstellen, können Sie dieselbe Datei im Pfad `/usr/share/nginx/html` innerhalb des Containers finden.

   > Das `ro` am Ende der Volume-Flag, getrennt durch `:`, steht für read-only. Wenn du es auf `rw` setzt, wird es les- und schreibbar.

4. Die `-p` oder `--port` Flag zuweist einen Port vom Hostsystem einem Port im Container.

   > In diesem Beispiel wird Port `8080` auf dem Hostsystem auf Port `80` im Container abgebildet.

3. Die `-d`-Option führt den Prozess im Hintergrund aus.

# Sanktionsarbeitumgehung

Um Sanktionen zu umgehen, können Sie die folgenden Methoden verwenden:

1. Mit DNS
2. Mit anderen Spiegeln
3. Mit Proxy-Client-Tools wie [Hiddify](https://hiddify.com/) und [Nekoray](https://github.com/MatsuriDayo/nekoray).

## Mit anderen Spiegeln

Die einfachste Methode, um Sanktionen zu umgehen, besteht darin, Bilder aus anderen Repositories wie focker.ir und ArvanCloud herunterzuladen.

ArvanCloud hat einen [umfassenden Leitfaden](https://www.arvancloud.ir/fa/dev/docker) dazu veröffentlicht.

Zusammenfassend können Sie den folgenden Befehl verwenden, um Bilder von ArvanCloud herunterzuladen:

```
docker pull docker.arvancloud.ir/<ImageName>
```

Ähnlich verhält es sich bei focker.ir:

```
docker pull focker.ir/<ImageName>
```

## Mit DNS

Mehrere interne DNS-Dienste sind verfügbar, um Sanktionen zu umgehen, darunter [Shecan](https://shecan.ir/), [403](https://403.online/) und [Begzar](https://begzar.ir/).

### Begzar

```
/etc/resolv.conf
 nameserver 185.55.226.26
 nameserver 185.55.225.25
```

### 403

```
/etc/resolv.conf
 nameserver 10.202.10.202
 nameserver 10.202.10.102
```

### Shecan

```
/etc/resolv.conf
 nameserver 178.22.122.100
 nameserver 185.51.200.2
```

# Docker Compose

[Docker Compose](https://docs.docker.com/compose/) ist eines der leistungsstärksten Tools von Docker und ermöglicht es Ihnen, Konfigurationen für mehrere Container in einer einzigen YAML-Datei zu definieren. Damit entfällt die Notwendigkeit, wiederholt Befehle im Terminal einzugeben oder Skripte manuell zu schreiben. Stattdessen können Sie alle Container mit einem einzigen Befehl starten.

# Flaggen

Docker bietet eine Reihe von Flags:

### --help

Zeigt Nutzungsinformationen und -befehle für Docker an.

### -D, --debug=true|false

Aktiviert oder deaktiviert den Debug Modus.

### -H, --host=[unix:///var/run/docker.sock]

Gibt die Socket Adresse für den Docker Dienst an.

### -l, --log-level=debug|info|warn|error|fatal

Legt die Protokollebene fest (Standardeinstellung ist Info).

### --tls=true|false

Gibt an, ob TLS verwendet werden soll (Standard ist falsch).

### --tlscacert=~/.docker/ca.pem

Stellt sicher, dass die Zertifikate von der angegebenen CA unterzeichnet werden.

### --tlscert=~/.docker/cert.pem

Gibt die Client Zertifikatdatei an.

### --tlskey=~/.docker/key.pem

Gibt die Clientschlüsseldatei an.

### --tlsverify=true|false

Aktiviert TLS und überprüft den Remote Zugriff.

### -v, --version=true|false

Zeigt die aktuelle Version von Docker an.

## Befehle

Verwenden Sie `docker --help`, um die Liste der verfügbaren Befehle zu überprüfen.

### run

Erstellen Sie einen neuen Container aus einem Image.

```
docker run hello-world
```

### exec

Führe Befehle in einem laufenden Container aus.

```
docker exec -it my_container bash
```

### ps

Listen Sie laufende Container auf.

```
docker ps
```

### build

Erstellen Sie ein Docker-Bild aus einer Dockerfile.

```
docker build -t my_image .
```

### pull

Laden Sie ein Bild von Docker Hub herunter.

```
docker pull nginx
```

### push

Laden Sie ein Bild in Docker Hub hoch.

```
docker push focker.ir/my_image
```

### images

Listen Sie verfügbare Bilder auf.

```
docker images
```

### login

Melden Sie sich bei Docker Hub an.

```
docker login
```

### logout

Melden Sie sich von Docker Hub aus.

```
docker logout
```

### search

Suche nach Bildern auf Docker Hub.

```
docker search redis
```

### version

Zeigen Sie die Docker-Version an.

```
docker version
```

### info

Systemweite Informationen anzeigen.

```
docker info
```

### attach

Befestigen Sie einen laufenden Behälter.

```
docker attach my_container
```

### commit

Erstellen Sie ein neues Bild aus den Änderungen eines Containers.

```
docker commit my_container my_image
```

### cp

Kopieren Sie Dateien zwischen einem Container und dem Host.

```
docker cp my_container:/path/in/container /path/on/host
```

### create

Erstellen Sie einen neuen Container.

```
docker create --name my_container ubuntu
```

### diff

Überprüfen Sie Änderungen an Dateien oder Verzeichnissen in einem Dateisystem eines Containers.

```
docker diff my_container
```

### events

Holen Sie sich Echtzeit-Ereignisse vom Docker-Server.

```
docker events
```

### export

Exportieren Sie das Dateisystem eines Containers als TAR -Archiv.

```
docker export my_container -o my_container.tar
```

### history

Zeigen Sie die Geschichte eines Bildes.

```
docker history ubuntu
```

### import

Erstellen Sie ein Bild aus einem Tarball.

```
docker import my_container.tar my_image
```
### inspect

Geben Sie niedrigstufige Informationen zu Docker-Objekten zurück.

```
docker inspect my_container
```

### kill

Töte einen laufenden Behälter.

```
docker kill my_container
```

### load

Laden Sie ein Bild aus einem Tar-Archiv.

```
docker load -i my_image.tar
```

### logs

Abrufen Sie die Protokolle eines Behälters ab.

```
docker logs my_container
```

### pause

Machen Sie alle Prozesse innerhalb eines oder mehrerer Container an.

```
docker pause my_container
```

### port

Listen Sie Port -Zuordnungen oder eine bestimmte Zuordnung für den Container auf.

```
docker port my_container
```

### rename

Benennen Sie einen Container um.

```
docker rename my_container new_container_name
```

### restart

Starten Sie einen Behälter neu.

```
docker restart my_container
```

### rm

Entfernen Sie einen oder mehrere Behälter.

```
docker rm my_container
```

### rmi

Entfernen Sie ein oder mehrere Bilder.

```
docker rmi my_image
```

### save

Speichern Sie ein oder mehrere Bilder in einem Tar-Archiv.

```
docker save -o my_image.tar my_image
```

### start

Starten Sie einen oder mehrere gestoppte Behälter.

```
docker start my_container
```

### stats

Eine Live-Übertragung der Ressourcennutzungsstatistiken von Container(n) anzeigen.

```
docker stats my_container
```

### stop

Beenden Sie einen oder mehrere laufende Container.

```
docker stop my_container
```

### tag

Erstellen Sie ein Tag für ein Bild.

```
docker tag my_image my_repo/my_image:tag
```

### top

Zeigen Sie die laufenden Prozesse eines Containers an.

```
docker top my_container
```

### unpause

Entpausiere alle Prozesse innerhalb eines oder mehrerer Container.

```
docker unpause my_container
```

### update

Aktualisieren Sie die Konfiguration eines oder mehrerer Container.

```
docker update --cpus=2 my_container
```

### wait

Warte, bis ein oder mehrere Container beendet werden, dann zeige ihre Exit-Codes an.

```
docker wait my_container
```
