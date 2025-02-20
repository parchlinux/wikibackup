---
title: Using your android phone as a webcam
description: 
published: true
date: 2024-07-29T18:39:45.995Z
tags: parch, parchlinux, scrcpy, webcam
editor: markdown
dateCreated: 2024-07-29T18:39:35.982Z
---

# How to use an android phone as a webcam in Parch Linux?


## Installing the dependencies

first of all you need to install some dependencies:

```bash
sudo pacman -S scrcpy dkms base-devel linux-headers v4l2loopback-dkms
```

then you need to load the module:

```bash
sudo modprobe v4l2loopback exclusive_caps=1
```

## Usage

### Camera Sharing

For using the front camera, first enable **usb debugging** in your phone, then connect your phone via cable and run this command in terminal:

```bash
scrcpy --video-source=camera --camera-size=1920x1080 --camera-facing=front --v4l2-sink=/dev/video0 --no-playback --no-window
```

For the back camera just change ```--camera-facing=front``` to ```--camera-facing=back``` .

#### testing camera

just open obs, or run this command:

```bash
ffplay /dev/video0
```

### mic sharing

For microphone you can run this command:

```bash
scrcpy --no-video --audio-source=mic --no-window
```

this would share your phone mic as system audio.


