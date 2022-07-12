---
description: Plutus Project Based Learning Virtual Machine Development environment
---

# Plutus PBL VM environment

Authored by Lucas

Test by Stephen

## Overview

This documentation describes the setup of a baseline Virtual Machine development environment for Plutus Project Based Learning version 2.

## Hardware requirements <a href="#docs-internal-guid-3b498049-7fff-bc94-b3e2-df824b7be1c7" id="docs-internal-guid-3b498049-7fff-bc94-b3e2-df824b7be1c7"></a>

* 4GB-8GB of RAM (ideally +4GB if you are running VirtualBox over Windows 10)
* PAB will require at least 16GB+
* 100Gb-200Gb of Storage

{% hint style="info" %}
Tested on AMD Ryzen 7 5700U Eight-Core, 16 GB RAM, 256 GB SSD, Windows 11
{% endhint %}

## VirtualBox installation

{% hint style="info" %}
**Oracle VM VirtualBox** supports the creation and management of guest virtual machines running Windows and Linux. Open Source software.
{% endhint %}

Download and install the latest release

{% embed url="https://www.virtualbox.org/" %}

![](<../.gitbook/assets/Screenshot 2022-07-12 140204.png>)

![](<../.gitbook/assets/Screenshot 2022-07-12 140331.png>)

{% hint style="info" %}
Accept file associations and creating shortcuts.
{% endhint %}

![](<../.gitbook/assets/Screenshot 2022-07-12 140820.png>)

![](<../.gitbook/assets/Screenshot 2022-07-12 142051.png>)

* [x] Installed with no issues - Windows 11 Stephen W

## V**isual Studio Code**

{% hint style="info" %}
**Visual Studio Code** is a streamlined code editor with support for development operations like debugging, task running, and version control.
{% endhint %}

Download Visual Studio Code - Mac, Linux, Windows

{% embed url="https://code.visualstudio.com/download" %}

For Linux Mint = .deb 64

Check architecture in terminal

```
- dpkg --print-architecture
```

Download .deb and install package from [https://linuxhint.com/install-visual-studio-code-linux-mint/](https://linuxhint.com/install-visual-studio-code-linux-mint/)

* [x] Visual Studio Code installed successfully

## NIX <a href="#docs-internal-guid-edaa4226-7fff-a526-70ff-686007764b89" id="docs-internal-guid-edaa4226-7fff-a526-70ff-686007764b89"></a>

{% hint style="info" %}
[Nix ](https://nixos.org/)is a tool that takes a unique approach to package management and system configuration. Learn how to make reproducible, declarative and reliable systems.
{% endhint %}

Follow the instructions for installing Nix and setting up cache in the link below

{% embed url="https://plutus-community.readthedocs.io/en/latest/#Environment/Build/Ubuntu/#_top" %}

{% hint style="info" %}
Keep in mind that the cache will download around 15Gb from IOG.&#x20;

We will take the single-user option.
{% endhint %}

Set the environment in this shell (or logout/login will achieve this)

```
. /home/osboxes/.nix-profile/etc/profile.d/nix.sh
```

Add IOG's caches to Nix

```
mkdir ~/.config/nix
echo 'substituters = https://hydra.iohk.io https://iohk.cachix.org https://cache.nixos.org/' >> ~/.config/nix/nix.conf
echo 'trusted-public-keys = hydra.iohk.io:f/Ea+s+dFdN+3Y/G+FDgSq+a5NEWhJGzdjvKNGv0/EQ= iohk.cachix.org-1:DpRUyj7h7V830dp/i6Nti+NEO2/nhblbov/8MW7Rqoo= cache.nixos.org-1:6NCHdD59X431o0gWypbMrAURkbJ16ZPMQFGspcDShjY=' >> ~/.config/nix/nix.conf
```





* NIX download - 18:29 UTC Finished 18:30 UTC&#x20;
* cat \~/.config/nix/nix.conf to confirm IOG's caches added to Nix&#x20;
* nix-env (Nix) 2.9.2 installed
