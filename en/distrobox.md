---
title: Distrobox
description: 
published: true
date: 2024-07-26T09:55:03.789Z
tags: distrobox, podman, docker
editor: markdown
dateCreated: 2024-07-26T09:52:59.311Z
---

# Distrobox	
> Distrobox is a container wrapping layer that allows the user to install containerised versions of Linux that are different to the host while providing tight integration with the host allowing the use of binaries designed for one distribution to run on another. 

Distrobox itself is not a container manager and relies on Podman or [Docker](https://wiki.parchlinux.com/en/docker) to create containers

From the Distrobox documentation:

> Use any Linux distribution inside your terminal. Enable both backward and forward compatibility with software and freedom to use whatever distribution you’re more comfortable with. Distrobox uses Podman or Docker to create containers using the Linux distribution of your choice. The created container will be tightly integrated with the host, allowing sharing of the HOME directory of the user, external storage, external USB devices and graphical apps (X11/Wayland), and audio.

## Security implications

The main goal of Distrobox is not focused on sandboxing the containers from the host and the containers that are running inside distrobox would have full access to your home folder as well as some other locations.

It is recommended to use **Podman** instead of **Docker** since by default docker would run containers as root and rootful containers **will have unrestricted access to your host filesystem**


## Installation

### With root access

first you need install either podman or docker to begin.

then install ```distrobox``` or ```distrobox-git``` from aur using paru.


### Without root access

It is possible to install Distrobox into your home folder if you don't have root access to the system or if you are using an immutable distro. Doing so requires the use of a curl-to-sh pipe which is an unsupported installation method due to it posing a security risk.

You can find instructions on the [Distrobox documentation page](https://distrobox.privatedns.org/#curl-or-wget)

## Usage
> Note:
> - Throughout the following section ‍‍‍```name``` is a variable and can be whatever you want. In all cases replace ```name``` with the actual name you choose
> - For the full list of supported options in any sub category use ```--help```, for example to see all creation options use ```distrobox create --help```
> - A full list of supported distros along with their image names can be found at https://distrobox.it/compatibility/#containers-distros
> - For more advanced usage techniques please see the Distrobox Documentation page at https://distrobox.it/usage/usage/

To create a new container run the following: 
```bash
distrobox create -n name
```

To List installed containers:
```bash
distrobox list
```

To intract with an installed container:
```bash
distrobox enter name
```
or you can run a command directly:
```bash
distrobox enter name -- command
```
To stop a running container run the following:

```
distrobox stop name
```
To delete a container run the following:

```
distrobox rm name
```
To install a specific distro into a container run the following (in this example its Ubuntu):

```
distrobox create --image ubuntu:22.04
```
Installations can be fully customised as follows (in this example its a container called test running Gentoo with root access):

```
distrobox create -i docker.io/gentoo/stage3:latest -n test --root
```

If you need your container to have root access to the host then it is recommended that you use the ‍‍‍```--root``` flag over ```sudo distrobox```


## Configuration
It is possible to configure Distrobox in two ways, either with a configuration file or by using environment variables. 

### Configuration files

Distrobox checks the following locations for config files, from least important to most important:

    /usr/share/distrobox/distrobox.conf
    /usr/etc/distrobox/distrobox.conf
    /etc/distrobox/distrobox.conf
    ~/.config/distrobox/distrobox.conf
    ~/.distroboxrc

An example config file is as follows: 

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

The following variables are available and should be set using per user variables:

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

