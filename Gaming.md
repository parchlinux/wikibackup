---
title: Gaming on Parch Linux
description: A simple Guide about Gaming on Parch Linux
published: true
date: 2025-03-30T17:48:34.701Z
tags: game, parchlinux, gaming, linux
editor: markdown
dateCreated: 2024-05-16T17:56:46.186Z
---

# Gaming on ParchLinux

Acording to Archlinux wiki:

> Linux has long been considered an "unofficial" gaming platform; the support and target audience provided to it is not a primary priority for most gaming organizations. Changes to this situation have accelerated, starting from 2021 onward, as big players like Valve, the CodeWeavers group and the community have made tremendous improvements to the ecosystem, allowing Linux to truly become a viable platform for gaming. Further, more and more indie development teams strive to use cross-platform rendering engines in order to have their game able to compile and run on Linux.
When it comes to gaming, the majority of user's thoughts are often directed towards popular AAA games which are usually written exclusively for the Microsoft Windows platform. This is understandable, however, it is not the only and sole availability. Please refer to #Game environments and #Getting games further down the page where you can find software to run games from other platforms.
If you however are fixated on getting games written for Microsoft Windows to work on Linux, then a different mindset, tools and approach is required; understanding internals and providing functional substitution. 


# Drivers

For better experience in Gaming you need to install some drivers on Parch Linux

## [Intel graphics](https://wiki.archlinux.org/title/Intel_graphics)

For Gen 3 hardware and later intel GPU install ```mesa```^extra^ ```lib32-mesa``` ^multilib^ and for Gen 2 to Gen 11 hardware install ```mesa-amber```^extra^ ```lib32-mesa-amber```^multilib^ .

The ```xf86-video-intel```^extra^ package provides the legacy intel DDX driver from Gen 2 to Gen 9 hardware. This package is generally not recommended.

## [vulkan](https://wiki.archlinux.org/title/Vulkan)

Here are the instructions for installing Vulkan drivers on Intel and AMD graphics cards:

### **For Intel GPUs:**

For Vulkan support (Haswell and newer; support for earlier chips is incomplete or missing), install the ```vulkan-intel```^extra^ package.
For 32-bit Vulkan support, install the ```lib32-vulkan-intel```^multilib^ package.

### **For Nvidia GPUs:**
For NVIDIA GPUs, there are two implementations available:

##### Proprietary Driver
- `nvidia-utils`^extra^ (or `lib32-nvidia-utils`^multilib^ for 32-bit support) 
- This is the proprietary driver provided by NVIDIA, which includes an OpenGL implementation.

##### Open-Source Driver
- `vulkan-nouveau`^extra^ (or `lib32-vulkan-nouveau`^multilib^ for 32-bit support) 
- This is the open-source NVK driver, which is part of the Mesa project. It provides a Vulkan implementation for NVIDIA GPUs.


### **For AMD GPUs:**
AMD offers two Vulkan driver options:

1. **vulkan-radeon**
    RADV (part of Mesa project)
    
Install ‍‍‍```vulkan-radeon```^extra^ package.


2. **amdvlk**
   AMDVLK Open (maintained by AMD)
   
Install ```amdvlk```^extra^

Additionally, for 32-bit application support, you can install the corresponding `lib32` packages:

- For `vulkan-radeon`: `lib32-vulkan-radeon`^multilib^
- For `amdvlk`: `lib32-amdvlk`^multilib^

After installing the appropriate Vulkan driver, your system should be able to run Vulkan-based applications and games seamlessly.

> ## [AMDGPU](https://wiki.archlinux.org/title/AMDGPU)

> ## [Nvidia](https://wiki.archlinux.org/title/NVIDIA)

## [Mesa](https://mesa3d.org/)
Mesa is an open-source OpenGL implementation, continually updated to support the latest OpenGL specification. It has a collection of open-source drivers for Intel graphics, AMD (formerly ATI), and NVIDIA GPUs. Mesa also provides software rasterizers, such as llvmpipe.

There are two Mesa packages, each with a distinct set of drivers:


### mesa
`mesa` is the up-to-date Mesa package which includes most of the modern drivers for newer hardware:

- `r300`: for AMD's Radeon R300, R400, and R500 GPUs.
- `r600`: for AMD's Radeon R600 GPUs up to Northern Islands. Officially supported by AMD.
- `radeonsi`: for AMD's Southern Island GPUs and later. Officially supported by AMD.
- `nouveau`: Nouveau is the open-source driver for NVIDIA GPUs.
- `virtio_gpu`: a virtual GPU driver for virtio, can be used with QEMU-based VMMs (like KVM or Xen).
- `vmwgfx`: for VMware virtual GPUs.
- `i915`: for Intel's Gen 3 hardware.
- `crocus`: for Intel's Gen 4 to Gen 7 hardware.
- `iris`: for Intel's Gen 8 hardware and later. Officially supported by Intel.
- `zink`: a Gallium driver used to run OpenGL on top of Vulkan.
- `d3d12`: for OpenGL 3.3 support on devices that only support D3D12 (i.e., WSL).
- `softpipe`: a software rasterizer and a reference Gallium driver.
- `llvmpipe`: a software rasterizer which uses LLVM for x86 JIT code generation and is multi-threaded.

### mesa-amber

`mesa-amber` is the legacy Mesa package which includes the classic (non-Gallium3D) drivers for older hardware:

- `i830`: for Intel's Gen 2 hardware. Same binary as `i965`.
- `i915`: for Intel's Gen 3 hardware. Same binary as `i965`.
- `i965`: for Intel's Gen 4 to Gen 11 hardware. Officially supported by Intel.
- `radeon`: for AMD's Radeon R100 GPUs. Same binary as `r200`.
- `r200`: for AMD's Radeon R200 GPUs.
- `nouveau_vieux`: for NVIDIA NV04 (Fahrenheit) to NV20 (Kelvin) GPUs.
- `swrast`: a legacy software rasterizer.

**Note:** When using Mesa, the correct driver should be selected automatically, thus no configuration is needed once the package is installed.

### Proprietary Drivers

- `nvidia-utils` is the proprietary driver for NVIDIA GPUs, which includes an OpenGL implementation.
- `amdgpu-pro-oglp` (AUR) is the proprietary driver for AMD GPUs.

# Gaming Platforms

## Steam
Steam is a popular game distribution platform by Valve. 
- for installation just install ```steam```^extra^ package.

## Proton
A compatibility layer that allows Steam to run Windows games on Linux.
We recommend installing Proton with the help of **ProtonUp-Qt**. 

## ProtonUp-Qt
A graphical utility for managing and installing different versions of Proton on Steam, allowing you to choose the best version for each game.
- for installation just install ```protonup-qt```^AUR^

## Proton-GE 
An optimized and extended version of Proton that provides better performance for running Windows games on Linux.
We recommend installing Proton with the help of **ProtonUp-Qt**. 

## [GameMode](https://wiki.archlinux.org/title/Gamemode)
A system utility that applies temporary optimizations to improve game performance on Linux.
- for installation just install ```gamemode```^extra^ ```lib32-gamemode```^extra^ packages

## Wine-GE 
An optimized and extended version of Wine **(the Windows compatibility layer for Linux)** that is tailored for running Windows games on Linux.
- for installation just install ```wine-ge-custom```^AUR^
## [Lutris](https://lutris.net/)
An all-in-one application for installing and running Windows and Linux games on Linux, supporting tools like Wine-GE and Proton.
- for installation just install ```lutris```^extra^

### Additional Tips
-  Check **[ProtonDB](https://www.protondb.com/)** for compatibility reports and tips on running games better.
-  To set the Proton version used in Steam for a game:
1. Right-click the game in your Steam library and select Properties.
2. Go to the Compatibility tab.
3. From the "Use this tool for compatibility" list, select the Proton version you want (e.g., Proton-GE).
-  To enable GameMode for a specific Steam game:
1. Right-click the game in your Steam library and select Properties.
2. Go to the Launch Options section.
3. In the text box, enter gamemoderun %command%.

> This guide will help you take advantage of ParchLinux's powerful gaming tools, allowing for seamless installation and gameplay. For more details on each tool, please refer to the official documentation
> 
{.is-success}



