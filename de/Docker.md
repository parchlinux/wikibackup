---
title: Docker
description: 
published: true
date: 2025-04-10T18:27:56.858Z
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

1. The `--name` flag assigns a name to the container, in this example, `some-nginx`.
2. The `-v` or `--volume` flag shares a (path on the host system) with (a path in the container).

   > In this example, the path `/some/content` on the host system is shared with `/usr/share/nginx/html` in the container. For instance, if you create a file named `name.txt` in `/some/content` on the host system, you can find the same file in `/usr/share/nginx/html` within the container.

   > The `ro` at the end of the volume flag, separated by `:`, stands for read-only. If you set it to `rw`, it will be read and write.

4. The `-p` or `--port` flag maps a port from the host system to a port in the container.

   > In this example, port `8080` on the host system is mapped to port `80` in the container.

3. The `-d` flag runs the process in the background.

# Sanctions Workaround

To bypass sanctions, you can use the following methods:

1. Using DNS
2. Using other mirrors
3. Using proxy client tools such as [Hiddify](https://hiddify.com/) and [Nekoray](https://github.com/MatsuriDayo/nekoray).

## Using Other Mirrors

The simplest method to bypass sanctions is to download images from other repositories, such as focker.ir and ArvanCloud.

ArvanCloud has published a [comprehensive guide](https://www.arvancloud.ir/fa/dev/docker) on this.

In summary, you can use the following command to download images from ArvanCloud:

```
docker pull docker.arvancloud.ir/<ImageName>
```

Similarly, for focker.ir:

```
docker pull focker.ir/<ImageName>
```

## Using DNS

Several internal DNS services are available to bypass sanctions, including [Shecan](https://shecan.ir/), [403](https://403.online/), and [Begzar](https://begzar.ir/).

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

[Docker Compose](https://docs.docker.com/compose/) is one of Docker's most powerful tools, enabling you to define configurations for multiple containers in a single YAML file. This avoids the need to repeatedly type commands in the terminal or manually write scripts. Instead, you can run all the containers with a single command.

# Flags

Docker provides a set of flags:

### --help

Displays usage information and commands for Docker.

### -D, --debug=true|false

Enables or disables debug mode.

### -H, --host=[unix:///var/run/docker.sock]

Specifies the socket address for the Docker service.

### -l, --log-level=debug|info|warn|error|fatal

Sets the log level (default is info).

### --tls=true|false

Specifies whether to use TLS (default is false).

### --tlscacert=~/.docker/ca.pem

Ensures that the certificates are signed by the specified CA.

### --tlscert=~/.docker/cert.pem

Specifies the client certificate file.

### --tlskey=~/.docker/key.pem

Specifies the client key file.

### --tlsverify=true|false

Enables TLS and verifies remote access.

### -v, --version=true|false

Displays the current version of Docker.

## Commands

Use `docker --help` to review the list of available commands.

### run

Run a new container from an image.

```
docker run hello-world
```

### exec

Execute commands in a running container.

```
docker exec -it my_container bash
```

### ps

List running containers.

```
docker ps
```

### build

Build a Docker image from a Dockerfile.

```
docker build -t my_image .
```

### pull

Download an image from Docker Hub.

```
docker pull nginx
```

### push

Upload an image to Docker Hub.

```
docker push focker.ir/my_image
```

### images

List available images.

```
docker images
```

### login

Log in to Docker Hub.

```
docker login
```

### logout

Log out of Docker Hub.

```
docker logout
```

### search

Search for images on Docker Hub.

```
docker search redis
```

### version

Display the Docker version.

```
docker version
```

### info

Display system-wide information.

```
docker info
```

### attach

Attach to a running container.

```
docker attach my_container
```

### commit

Create a new image from a container's changes.

```
docker commit my_container my_image
```

### cp

Copy files between a container and the host.

```
docker cp my_container:/path/in/container /path/on/host
```

### create

Create a new container.

```
docker create --name my_container ubuntu
```

### diff

Inspect changes to files or directories on a container’s filesystem.

```
docker diff my_container
```

### events

Get real-time events from the Docker server.

```
docker events
```

### export

Export a container’s filesystem as a tar archive.

```
docker export my_container -o my_container.tar
```

### history

Show the history of an image.

```
docker history ubuntu
```

### import

Create an image from a tarball.

```
docker import my_container.tar my_image
```
### inspect

Return low-level information on Docker objects.

```
docker inspect my_container
```

### kill

Kill a running container.

```
docker kill my_container
```

### load

Load an image from a tar archive.

```
docker load -i my_image.tar
```

### logs

Fetch the logs of a container.

```
docker logs my_container
```

### pause

Pause all processes within one or more containers.

```
docker pause my_container
```

### port

List port mappings or a specific mapping for the container.

```
docker port my_container
```

### rename

Rename a container.

```
docker rename my_container new_container_name
```

### restart

Restart a container.

```
docker restart my_container
```

### rm

Remove one or more containers.

```
docker rm my_container
```

### rmi

Remove one or more images.

```
docker rmi my_image
```

### save

Save one or more images to a tar archive.

```
docker save -o my_image.tar my_image
```

### start

Start one or more stopped containers.

```
docker start my_container
```

### stats

Display a live stream of container(s) resource usage statistics.

```
docker stats my_container
```

### stop

Stop one or more running containers.

```
docker stop my_container
```

### tag

Create a tag for an image.

```
docker tag my_image my_repo/my_image:tag
```

### top

Display the running processes of a container.

```
docker top my_container
```

### unpause

Unpause all processes within one or more containers.

```
docker unpause my_container
```

### update

Update configuration of one or more containers.

```
docker update --cpus=2 my_container
```

### wait

Block until one or more containers stop, then print their exit codes.

```
docker wait my_container
```
