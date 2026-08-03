---
title: Package Management
description: 
published: true
date: 2024-05-05T15:19:05.888Z
tags: 
editor: markdown
dateCreated: 2024-05-05T14:49:35.443Z
---

# Package Management in Parch Linux

## Package Manager

The package manager in Parch Linux is called pacman.

Acording to The ArchLinux wiki:

>The pacman package manager is one of the major distinguishing features of Arch Linux. It combines a simple binary package format with an easy-to-use build system. The goal of pacman is to make it possible to easily manage packages, whether they are from the official repositories or the user's own builds.
Pacman keeps the system up-to-date by synchronizing package lists with the master server. This server/client model also allows the user to download/install packages with a simple command, complete with all required dependencies.
Pacman is written in the C programming language and uses the bsdtar(1) tar format for packaging.


## How does pacman works?

Here is a small cheatsheet that helps you to use pacman:

## Basic operations

| Action | Arch | Red Hat/Fedora | Debian/Ubuntu | SLES/openSUSE | Gentoo |
|--------|------|-----------------|----------------|-----------------|--------|
| Search for package(s) | `pacman -Ss` | `dnf search` | `apt search` | `zypper search` or `zypper se [-s]` | `emerge --search` (`-s`) or `emerge --searchdesc` (`-S`) |
| Install package(s) by name | `pacman -S` | `dnf install` | `apt install` | `zypper install` or `zypper in` | `emerge` |
| Get source package(s) and build dependencies | `makepkg -s PKGBUILD` | `dnf builddep` | `apt build-dep` | `zypper source-install` (`zypper si`) or `zypper install -d` | `emerge`, or explicitly `emerge --with-bdeps` |
| Print targets without performing the operation | `pacman --print` (or `-p`) | `dnf --setopt=tsflags=test` | `apt --simulate` (or `-s`, `--dry-run`, `--just-print`) | `zypper --dry-run` | `emerge --pretend` (`-p`) |
| Toggle confirmations | `pacman --confirm` or `pacman --noconfirm` | `dnf --assumeyes` (`-y`) or `dnf --assumeno` | `apt --yes` (`-y`) | `zypper --non-interactive` (`-n`) or `zypper --no-confirm` (`-y`) | `emerge --ask` (`-a`) |
| Refresh local package repository | `pacman -Sy` | `dnf check-update` or `dnf makecache` or `dnf upgrade` | `apt update` | `zypper refresh` or `zypper ref` `[-s]` | `emerge --sync` |
| Upgrade Packages | `pacman -Syu` | `dnf upgrade` | `apt upgrade` | `zypper update` or `zypper up` | `emerge -[a]uDN @world` |
| Upgrade Packages (complex updates) | `pacman -Syu` | `dnf distro-sync` | `apt dist-upgrade` | `zypper dup` | `emerge -[a]uDN @world` |
| Remove a package(s) and dependencies | `pacman -Rs` | `dnf remove` | `apt autoremove` | `zypper remove` or `zypper rm` | `emerge --depclean` (`-c`) |
| Remove package(s) and configuration files | `pacman -Rn` | ? | `apt purge` | ? | n/a |
| Remove package(s), dependencies, and config files | `pacman -Rns` | ? | `apt autoremove --purge` | ? | n/a |
| Remove unneeded dependencies | `pacman -Qdtq | pacman -Rs -` `` (`-Qdttq` for optional deps)| `dnf autoremove` | `apt autoremove` | `zypper rm -u` or `zypper packages --unneeded` | `emerge --depclean` (`-c`) |
| Remove packages not in repositories | ```pacman -Rs $(pacman -Qmq)```  | `dnf repoquery --extras` | `aptitude purge '~o'` || ? |
| Mark installed package as explicitly required | `pacman -D --asexplicit` | `dnf mark install` | `apt-mark manual` | `zypper install --force` | `emerge --select` (`-w`) |
| Install package(s) as dependency | `pacman -S --asdeps` | `dnf install` then `dnf mark remove` | `apt-mark auto` | n/a ([workaround](https://bugzilla.opensuse.org/show_bug.cgi?id=1175678)) | `emerge --oneshot` (`-1`) |
| Only download package(s) | `pacman -Sw` | `dnf download` | `apt install --download-only` or `apt download` | `zypper --download-only` | `emerge --fetchonly` (`-f`) |
| Clean up local caches | `pacman -Sc` or `pacman -Scc` | `dnf clean all` | `apt autoclean` or `apt clean` | `zypper clean` | `eclean distfiles` |
| Start a shell | | `dnf shell` | | `zypper shell` ||

## Querying specific packages

| Action | Arch | Red Hat/Fedora | Debian/Ubuntu | SLES/openSUSE | Gentoo |
|--------|------|-----------------|----------------|-----------------|--------|
| Show package information | `pacman -Si` or `pacman -Qi` | `dnf list` or `dnf info` | `apt show` or `apt-cache policy` | `zypper info` or `zypper if` | `emerge -S`, `emerge -pv` or `eix` |
| Display local package info | `pacman -Qi` | `rpm -qi` / `dnf info installed` | `dpkg -s` or `aptitude show` | `zypper --no-remote info` or `rpm -qi` | `emerge -pv` or `emerge -S` |
| Display remote package info | `pacman -Si` | `dnf info` | `apt-cache show` or `aptitude show` | `zypper info` | `emerge -pv` and `emerge -S` or `equery meta` |
| Display local package files | `pacman -Ql` | `rpm -ql` | `dpkg -L` | `rpm -ql` | `equery files` or `qlist` |
| Display remote package files | `pacman -Fl` | `dnf repoquery -l` or `repoquery -l` | `apt-file list` || `pfl` |
| Query package providing file | `pacman -Qo` | `rpm -qf` (installed) or `dnf provides` (everything) or `repoquery -f` | `dpkg -S` or `dlocate` | `rpm -qf` (installed) or `zypper search -f` (everything) | `equery belongs` or `qfile` |
| List files in package | `pacman -Ql` or `pacman -Fl` | `dnf repoquery -l` | `dpkg-query -L` | `rpm -ql` | `equery files` or `qlist` |
| Show reverse provides | `pacman -F` | `dnf provides` | `apt-file search` | `zypper what-provides` or `zypper wp` (exact)

 or `zypper se --provides` (fuzzy) | `equery belongs` (installed) or `pfl` |
| Search package by file | `pacman -F` | `dnf provides` | `apt-file search` or `auto-apt` | `zypper search -f` | `equery belongs` or `qfile` |
| Show package changelog | `pacman -Qc` | `dnf changelog` | `apt-get changelog` | `rpm -q --changelog` | `equery changes -f` |



## AUR

> The Arch User Repository (AUR) is a community-driven repository for Arch users. It contains package descriptions (PKGBUILDs) that allow you to compile a package from source with makepkg and then install it via pacman. The AUR was created to organize and share new packages from the community and to help expedite popular packages' inclusion into the extra repository.
A good number of new packages that enter the official repositories start in the AUR. In the AUR, users are able to contribute their own package builds (PKGBUILD and related files). The AUR community has the ability to vote for packages in the AUR. If a package becomes popular enough — provided it has a compatible license and good packaging technique — it may be entered into the extra repository (directly accessible by pacman or from the Arch build system). 


### AUR Manager

Parch Linux has Paru as is AUR Manager.
using Paru is just like using pacman, with the same syntax you can easly install packages from AUR.


#### Using Paru
Here are some useful paru commands:

| Command | Description |
| --- | --- |
| `paru` | Update the entire system |
| `paru -Syu` | Update the entire system |
| `paru -S appname` | Install the program from AUR |
| `paru appname` | Install the program from AUR, choosing from the list |
| `paru -Sc` | Remove Pacman and Paru caches |
| `paru -Ss appname` | Search for a package |

