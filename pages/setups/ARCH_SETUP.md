---
index: 16
---
# ARCH LINUX PERSONAL SETUP

over the years i have customized a lot my arch linux installation and pushed by the fear of loosing all my customization i've pushed all of my dotfiles in a [github repo](https://github.com/carnivuth/scripts).

Why i wrote this page? because i am lazy basically, and the idea of re-imagine the steps to reconfigure a new machine (*or this machine if for some reason i need to reconfigure it*) it's too much on my mental stack and prevents me from even start the process, so the idea is:

```mermaid
flowchart LR
A[insert USB stick]
B[clone this repo]
C["`**GREP AND PASTE LIKE THERE IS NO TOMORROW**`"]
A --> B --> C
```

## STEPS

- Download latest arch  ISO from the [official website](https://archlinux.org/download/)

- write the image to a USB pen

```bash
dd if=/Downloads/archlinux.iso of=/dev/<usb pen> status=progress
```

### INSIDE LIVE ENVIRONMENT

- connect to network

```bash
iwctl station wlan0 connect <BSSID>
```

- setup `pacman` parallel downloads and update local db info

```bash
pacman -Sy
pacman -S sed
sed -i 's/#ParallelDownloads.*/ParallelDownloads = 16/g' '/etc/pacman.conf'
```

- install git and vim

```bash
pacman -S git vim
```

- run the official installation script

```bash
archinstall --config user_configuration.json --creds user_credentials.json
```

### INSIDE THE INSTALLED SYSTEM

- configure `greetd`

```bash
pacman -S sed
sed -i 's|command.*/command = "agretty --cmd /bin/Hyprland"/g' '/etc/greetd/config.toml'
```

- authenticate to `github`

```bash
gh auth login
```
[PREVIOUS](pages/utils/MATHJAX_CHEETSHEET.md) [NEXT](pages/setups/ANDROID_SETUP.md)
