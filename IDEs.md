---
title: IDEs in Parch
description: Introduction and tutorial for installing popular IDEs on Parch Linux
published: true
date: 2025-02-13T07:51:44.751Z
tags: ide, ides, vscode, code, jetbrains, editor, development, programing
editor: markdown
dateCreated: 2025-02-08T12:54:47.718Z
---

# Integrated Development Environment (IDE)

## Overview
Integrated Development Environments (IDEs) are environments that include a text editor, project management tools, a debugger, and other tools for software development.

## Popular IDEs

### 1. **Visual Studio Code**
Visual Studio Code (VS Code) is one of the most popular and widely used code editors developed by Microsoft.

#### Available Versions:
- **Code - OSS**: The official open-source package from Arch Linux. This version includes a configuration to enable [Open VSX](https://open-vsx.org/).  
  **Installation:**
  ```bash
  sudo pacman -S code
  ```

- **Visual Studio Code**: The proprietary version owned by Microsoft.  
  **Installation:**
  ```bash
  yay -S visual-studio-code-bin
  ```

- **VSCodium**: A community-driven free version that does not send telemetry data to service providers and provides [Open VSX](https://open-vsx.org/) support.  
  **Installation:**
  ```bash
  yay -S vscodium
  ```

### 2. **JetBrains IntelliJ IDEA**
IntelliJ IDEA is a professional IDE for Java software development. It offers powerful features for code development, project management, and testing.  
**Installation:**
```bash
sudo pacman -S intellij-idea-community-edition
```

### 3. **Eclipse**
Eclipse is a free IDE for Java software development that supports multiple programming languages.  
**Installation:**
```bash
sudo pacman -S eclipse-java-bin
```

### 4. **PyCharm**
PyCharm is a dedicated IDE for the Python programming language developed by JetBrains.  
**Installation:**
```bash
sudo pacman -S pycharm-community-edition
```

### 5. **Zed**
Zed is a new code editor built with the Rust programming language, focusing on speed, collaboration, and artificial intelligence (AI), supporting various programming languages.  
**Installation:**
```bash
sudo pacman -S zed
```

### 6. **Atom/Pulsar**
Pulsar is an open-source text editor that continues the development of Atom after GitHub officially ceased its development. It is designed for a lightweight and customizable experience.  
**Installation:**
```bash
yay -S pulsar
```

### 7. **NetBeans**
NetBeans is a free and powerful IDE developed by Oracle, primarily designed for Java software development. It also supports other programming languages.  
**Installation:**
```bash
sudo pacman -S netbeans
```

### 8. **All JetBrains products**
JetBrains Toolbox is a tool that allows you to easily manage and install JetBrains IDEs, such as IntelliJ IDEA, PyCharm, WebStorm, and more. It provides automatic updates and the ability to switch between different versions of JetBrains products.
**Installation:**
```bash
sudo pacman -S jetbrains-toolbox
```

### 9. **Vim/NeoVim**
NeoVim alone is not a complete IDE, but with the use of numerous plugins developed for it, it can be transformed into a development environment similar to an IDE.  
> For more details about NeoVim and how to convert it into a full-fledged IDE, you can refer to the [NeoVim page](https://wiki.parchlinux.com/en/neovim) in the Parch Wiki.
{.is-info}