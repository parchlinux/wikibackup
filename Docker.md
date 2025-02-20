---
title: Docker
description: 
published: true
date: 2024-07-26T10:03:09.866Z
tags: 
editor: markdown
dateCreated: 2024-07-26T10:03:03.792Z
---

# Docker Overview

Docker is a tool for containerization, enabling the sharing of development environments across various operating systems through containers. This accelerates development time and allows team members to share environments without dependency conflicts, as all dependencies are contained and isolated within the container.

# History
Before the concept of containers and environment isolation, virtualization was the main solution for separating development environments from the host system. Users would allocate CPU, memory, and hard space resources to a virtual system, but this approach was not optimal because a significant amount of resources was consumed by the virtual operating system, resulting in slower processing speeds compared to the host system.

With the advent of containers, isolation and separation of different environments became more cost-effective and resource-efficient. Docker is one of the tools that can be used for building and managing containers. If you need to share your development/production environment with others, Docker facilitates this by allowing you to share your container skeleton file (image), speeding up the process. Additionally, other users don’t need to worry about resolving dependencies as they are already included in the container.

# Installation and Setup

The [Docker documentation](https://docs.docker.com/engine/install/) provides comprehensive installation instructions for Linux systems. However, distributions based on Arch Linux are not officially supported and the installation is considered unstable.

1. Open your terminal and install Docker using the package manager:

   ```
   sudo pacman -S docker
   ```
   > If you encounter the error `docker not found`, make sure to update your repositories with the command `sudo pacman -Syu`.

2. If you are using systemd as your init system, enable the Docker service with:

   ```
   sudo systemctl enable --now docker.service
   ```

3. Add your username to the Docker group:

   ```
   sudo usermod -aG docker $USER
   ```
   > To apply the changes, either log out and log back in or use the command `newgrp docker`.

4. Verify the Docker installation by running the hello-world image:

   ```
   docker run hello-world
   ```

The `run` command executes images, which are blueprints for containers that consist of predefined files and configurations.

To list the images on your system, use `docker images`.

To list active containers, use `docker ps`.

# Docker Hub

[Docker Hub](https://hub.docker.com/) serves as Docker's default repository for downloading and uploading images.

For example, if you want to use nginx as your web server, you can download the nginx image from Docker Hub and create a container from it.

1. Log in to your Docker Hub account with:

   ```
   docker login
   ```
   > If you don't have an account, create one [here](https://app.docker.com/signup).

2. Download the latest nginx image with:

   ```
   docker pull nginx
   ```

   > Unfortunately, Docker Hub is blocked in Iran. If you encounter a 403 error or connection timeout, it is likely due to these restrictions. Refer to the [sanctions workaround](#sanctions-workaround) to resolve this issue.

   > nginx web server has [comprehensive documentation](https://wiki.parchlinux.com/fa/Docker) on Docker Hub about working with images and containers.

After downloading the image, create a container for nginx with:

```
docker run --name some-nginx -p 8080:80 -v /some/content:/usr/share/nginx/html:ro -d nginx
```

> If you are using other mirrors like focker.ir to download images, replace `nginx` with `focker.ir/nginx`.

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
