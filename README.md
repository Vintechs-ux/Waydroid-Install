# Waydroid Installation Guide for Arch Linux

A comprehensive guide to setting up Waydroid on Arch Linux for running Android applications seamlessly.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Installation](#installation)
  - [1. Install Dependencies](#1-install-dependencies)
  - [2. Install Waydroid](#2-install-waydroid)
  - [3. Configure Kernel Modules](#3-configure-kernel-modules)
  - [4. Initialize Waydroid](#4-initialize-waydroid)
  - [5. Start Waydroid Service](#5-start-waydroid-service)
  - [6. Launch Android Interface](#6-launch-android-interface)
- [Optional Configuration](#optional-configuration)
  - [Google Play Services](#google-play-services)
  - [GPU Acceleration](#gpu-acceleration)
- [Troubleshooting](#troubleshooting)
- [References](#references)

## Prerequisites
- Arch Linux system with full disk access
- Active internet connection
- AUR helper installed (yay/paru recommended)
- Wayland compositor (required for Waydroid)

## Installation

### 1. Install Dependencies
```bash
sudo pacman -S git base-devel wget python-pyxdg lzip
```

### 2. Install Waydroid
Using AUR helper:
```bash
yay -S waydroid
```

Manual installation from AUR:
```bash
git clone https://aur.archlinux.org/waydroid.git
cd waydroid
makepkg -si
```

### 3. Configure Kernel Modules
Ensure kernel modules are loaded:
```bash
sudo modprobe binder_linux
sudo modprobe ashmem_linux
```

For kernels <5.18:
```bash
yay -S linux-zen linux-zen-headers
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

### 4. Initialize Waydroid
```bash
sudo waydroid init
```

### 5. Start Waydroid Service
```bash
sudo systemctl start waydroid-container
sudo systemctl enable waydroid-container
```

### 6. Launch Android Interface
```bash
waydroid session start
waydroid show-full-ui
```

## Optional Configuration

### Google Play Services
```bash
yay -S waydroid-gapps
sudo waydroid upgrade
sudo systemctl restart waydroid-container
```

### GPU Acceleration
```bash
waydroid prop set persist.waydroid.opengl_mode gl
```

## Troubleshooting
- **Kernel modules not loading**:  
  Verify with `lsmod | grep -e binder -e ashmem`
  
- **Wayland compatibility**:  
  Ensure you're using a Wayland compositor (Weston/Sway/GNOME Wayland)

- **Container issues**:  
  Reset container with:
  ```bash
  sudo waydroid container stop
  sudo systemctl restart waydroid-container
  ```

## References
- [Official Waydroid Documentation](https://docs.waydro.id/)
- [Arch Linux Wiki](https://wiki.archlinux.org/title/Waydroid)
- [Waydroid GitHub Repository](https://github.com/waydroid/waydroid)
```
