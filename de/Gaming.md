---
title: Gaming auf Parch Linux
description: 
published: true
date: 2024-10-17T16:54:54.697Z
tags: game, parchlinux, gaming, linux
editor: markdown
dateCreated: 2024-10-17T16:54:51.193Z
---

# Gaming auf Parch Linux

Laut Archlinux-Wiki:

> Linux galt lange Zeit als „inoffizielle“ Gaming-Plattform; die Unterstützung und Zielgruppe, die es bietet, haben für die meisten Gaming-Organisationen keine oberste Priorität. Die Änderungen dieser Situation haben sich ab 2021 beschleunigt, da große Player wie Valve, die CodeWeavers-Gruppe und die Community enorme Verbesserungen am Ökosystem vorgenommen haben, wodurch Linux wirklich zu einer brauchbaren Plattform für Gaming wurde. Darüber hinaus bemühen sich immer mehr Indie-Entwicklungsteams, plattformübergreifende Rendering-Engines zu verwenden, damit ihre Spiele unter Linux kompiliert und ausgeführt werden können. 
Wenn es um Gaming geht, richten sich die Gedanken der meisten Benutzer oft auf beliebte AAA-Spiele, die normalerweise exklusiv für die Microsoft Windows-Plattform geschrieben werden. Das ist verständlich, es ist jedoch nicht die einzige und alleinige Verfügbarkeit. Bitte lesen Sie weiter unten auf der Seite #Spielumgebungen und #Spiele abrufen, wo Sie Software zum Ausführen von Spielen von anderen Plattformen finden. 
Wenn Sie jedoch darauf fixiert sind, Spiele, die für Microsoft Windows geschrieben wurden, unter Linux laufen zu lassen, dann sind eine andere Denkweise, andere Tools und ein anderer Ansatz erforderlich: Verständnis der internen Vorgänge und Bereitstellung eines funktionalen Ersatzes.


# Drivers

Für ein besseres Gaming-Erlebnis müssen Sie einige Treiber auf Parch Linux installieren

## [Intel graphics](https://wiki.archlinux.org/title/Intel_graphics)

Installieren Sie für Hardware der 3. Generation und spätere Intel-GPUs ```mesa```^extra^ ```lib32-mesa``` ^multilib^ und für Hardware der 2. bis 11. Generation installieren Sie ```mesa-amber```^extra^ ```lib32-mesa-amber```^multilib^.

Das Paket ```xf86-video-intel```^extra^ stellt den älteren Intel DDX-Treiber für Hardware der Generation 2 bis 9 bereit. Dieses Paket wird im Allgemeinen nicht empfohlen.

## [vulkan](https://wiki.archlinux.org/title/Vulkan)

Hier finden Sie die Anweisungen zur Installation von Vulkan-Treibern auf Intel- und AMD-Grafikkarten:

### **Für Intel GPUs:**

Installieren Sie für Vulkan-Unterstützung (Haswell und neuer; die Unterstützung für frühere Chips ist unvollständig oder fehlt) das Paket ```vulkan-intel``` ^extra^.
Installieren Sie für 32-Bit-Vulkan-Unterstützung das Paket ```lib32-vulkan-intel```^multilib^.

### **Für Nvidia GPUs:**
Für NVIDIA-GPUs stehen zwei Implementierungen zur Verfügung:

##### Proprietärer Driver
- `nvidia-utils`^extra^ (oder `lib32-nvidia-utils`^multilib^ für 32-Bit-Unterstützung) 
- Dies ist der proprietäre Treiber von NVIDIA, der eine OpenGL-Implementierung enthält.

##### Open-Source Driver
- `vulkan-nouveau`^extra^ (oder `lib32-vulkan-nouveau`^multilib^ für 32-Bit-Unterstützung) 
- Dies ist der Open-Source-NVK-Treiber, der Teil des Mesa-Projekts ist. Er bietet eine Vulkan-Implementierung für NVIDIA-GPUs.


### **Für AMD GPUs:**
AMD bietet zwei Vulkan-Treiberoptionen:

1. **vulkan-radeon**
    RADV (Teil des Mesa-Projekts)
    
Installieren Sie das Paket ‍‍‍```vulkan-radeon```^extra^.


2. **amdvlk**
   AMDVLK Open (gepflegt von AMD)
   
Installieren ```amdvlk```^extra^

Darüber hinaus können Sie zur Unterstützung von 32-Bit-Anwendungen die entsprechenden `lib32` Pakete installieren:
- für `vulkan-radeon`: `lib32-vulkan-radeon`^multilib^
- für `amdvlk`: `lib32-amdvlk`^multilib^

Nach der Installation des entsprechenden Vulkan-Treibers sollte Ihr System in der Lage sein, Vulkan-basierte Anwendungen und Spiele reibungslos auszuführen.

> ## [AMDGPU](https://wiki.archlinux.org/title/AMDGPU)

> ## [Nvidia](https://wiki.archlinux.org/title/NVIDIA)

## [Mesa](https://mesa3d.org/)
Mesa ist eine Open-Source-OpenGL-Implementierung, die ständig aktualisiert wird, um die neueste OpenGL-Spezifikation zu unterstützen. Es verfügt über eine Sammlung von Open-Source-Treibern für Intel-Grafiken, AMD (früher ATI) und NVIDIA-GPUs. Mesa bietet auch Software-Rasterizer wie llvmpipe.

Es gibt zwei Mesa-Pakete, jedes mit einem unterschiedlichen Treibersatz:


### mesa
`mesa` ist das aktuelle Mesa-Paket, das die meisten modernen Treiber für neuere Hardware enthält:

- `r300`: für AMDs Radeon R300, R400, und R500 GPUs.
- `r600`: für AMDs Radeon R600 GPUs bis Northern Islands. Offiziell von AMD unterstützt.
- `radeonsi`: für AMDs Southern Island GPUs und höher. Offiziell von AMD unterstützt.
- `nouveau`: Nouveau ist der Open-Source-Treiber für NVIDIA-GPUs.
- `virtio_gpu`: ein virtueller GPU-Treiber für Virtio, kann mit QEMU-basierten VMMs (wie KVM oder Xen) verwendet werden.
- `vmwgfx`: für virtuelle VMware-GPUs.
- `i915`: für Intels Gen 3-Hardware.
- `crocus`: für Intels Hardware der 4. bis 7. Generation.
- `iris`: für Intel-Hardware der 8. Generation und höher. Offiziell von Intel unterstützt.
- `zink`: Ein Gallium-Treiber, der zum Ausführen von OpenGL auf Vulkan verwendet wird.
- `d3d12`: für OpenGL 3.3-Unterstützung auf Geräten, die nur D3D12 unterstützen (d. h. WSL).
- `softpipe`: ein Software-Rasterizer und ein Referenz-Gallium-Treiber.
- `llvmpipe`: ein Software-Rasterizer, der LLVM zur x86-JIT-Codegenerierung verwendet und über mehrere Threads verfügt.

### mesa-amber

`mesa-amber` ist das alte Mesa-Paket, das die klassischen (nicht Gallium3D-)Treiber für ältere Hardware enthält:

- `i830`: für Intels Gen 2-Hardware. Gleiche Binärdatei wie `i965`. 
- `i915`: für Intels Gen 3-Hardware. Gleiche Binärdatei wie `i965`. 
- `i965`: für Intels Gen 4- bis Gen 11-Hardware. Offiziell von Intel unterstützt. 
- `radeon`: für AMDs Radeon R100-GPUs. Gleiche Binärdatei wie `r200`. 
- `r200`: für AMDs Radeon R200-GPUs. 
- `nouveau_vieux`: für NVIDIA NV04 (Fahrenheit) bis NV20 (Kelvin) GPUs. 
- `swrast`: ein veralteter Software-Rasterizer.

**Hinweis:** Bei Verwendung von Mesa sollte der richtige Treiber automatisch ausgewählt werden, sodass nach der Installation des Pakets keine Konfiguration erforderlich ist.

### Proprietärer Drivers

- `nvidia-utils` ist der proprietäre Treiber für NVIDIA-GPUs, der eine OpenGL-Implementierung enthält. 
- `amdgpu-pro-oglp` (AUR) ist der proprietäre Treiber für AMD-GPUs.

# Gaming-Plattformen

## Steam
Steam ist eine beliebte Spielevertriebsplattform von Valve.
- Installieren Sie zur Installation einfach das Paket ```steam```^extra^.

## Proton
Eine Kompatibilitätsebene, die es Steam ermöglicht, Windows-Spiele unter Linux auszuführen.
Wir empfehlen die Installation von Proton mit Hilfe von **ProtonUp-Qt**. 

## ProtonUp-Qt
Ein grafisches Dienstprogramm zum Verwalten und Installieren verschiedener Versionen von Proton auf Steam, mit dem Sie für jedes Spiel die beste Version auswählen können.
- zur Installation einfach installieren ```protonup-qt```^AUR^

## Proton-GE 
Eine optimierte und erweiterte Version von Proton, die eine bessere Leistung zum Ausführen von Windows-Spielen unter Linux bietet.
Wir empfehlen die Installation von Proton mit Hilfe von **ProtonUp-Qt**. 

## [GameMode](https://wiki.archlinux.org/title/Gamemode)
Ein Systemdienstprogramm, das temporäre Optimierungen anwendet, um die Spieleleistung unter Linux zu verbessern.
- zur Installation einfach installieren ```gamemode```^extra^ ```lib32-gamemode```^extra^ packages

## Wine-GE 
Eine optimierte und erweiterte Version von Wine **(der Windows-Kompatibilitätsschicht für Linux)**, die auf das Ausführen von Windows-Spielen unter Linux zugeschnitten ist.
- zur Installation einfach installieren ```wine-ge-custom```^AUR^
## [Lutris](https://lutris.net/)
Eine All-in-One-Anwendung zum Installieren und Ausführen von Windows- und Linux-Spielen unter Linux, die Tools wie Wine-GE und Proton unterstützt.
- zur Installation einfach installieren ```lutris```^extra^

### Zusätzliche Tipps
- Prüfen Sie **[ProtonDB](https://www.protondb.com/)** auf Kompatibilitätsberichte und Tipps zum besseren Ausführen von Spielen. 
- So legen Sie die in Steam für ein Spiel verwendete Proton-Version fest: 
1. Klicken Sie mit der rechten Maustaste auf das Spiel in Ihrer Steam-Bibliothek und wählen Sie Eigenschaften. 
2. Gehen Sie zur Registerkarte Kompatibilität. 
3. Wählen Sie aus der Liste „Dieses Tool für Kompatibilität verwenden“ die gewünschte Proton-Version aus (z. B. Proton-GE).
- So aktivieren Sie den GameMode für ein bestimmtes Steam-Spiel: 
1. Klicken Sie mit der rechten Maustaste auf das Spiel in Ihrer Steam-Bibliothek und wählen Sie „Eigenschaften“. 
2. Gehen Sie zum Abschnitt „Startoptionen“. 
3. Geben Sie in das Textfeld gamemoderun %command%“ ein.

> Mit dieser Anleitung sollten Sie in der Lage sein, die leistungsstarken Gaming-Tools von ParchLinux zu nutzen, um Spiele problemlos zu installieren und zu spielen. Weitere Informationen finden Sie in der offiziellen Dokumentation der einzelnen Tools.
> 
{.is-success}



