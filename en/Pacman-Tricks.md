---
title: Pacman Tricks
description: Useful tricks you should know for Pacman
published: false
date: 2024-10-20T12:56:18.952Z
tags: tips, tricks, pacman
editor: markdown
dateCreated: 2024-10-20T12:55:19.914Z
---

## About `pacman` command

[`pacman`](https://wiki.archlinux.org/title/Pacman) [package manager](https://en.wikipedia.org/wiki/Package_manager) is one of the most used commands in Arch Linux (or every other Arch-based distros).

> It combines a simple binary package format with an easy-to-use [Arch build system](https://wiki.archlinux.org/title/Arch_build_system). The goal of *pacman* is to make it possible to easily manage packages, whether they are from the [official repositories](https://wiki.archlinux.org/title/Official_repositories) or the user's own builds.

Pacman keeps your system up-to-date by syncing package lists with the master mirror server.

Read more about [*pacman* in Arch Linux Wiki](https://wiki.archlinux.org/title/Pacman).

## Removing unused packages (orphans)

> Orphans are packages that were installed as a dependency and are no longer required by any package.

For example, you may install a package (`package-one`) that requires `package-two` as a dependency. After some time, you may remove the `package-one`, but the `package-two` is still available on your system, though no other package is dependent on that.

In the example above, the `package-two` is an orphan package, because neither the user or any other package uses it.

There's a nice way to view the list of these orphan packages: