# Lenovo ThinkPad T480 - OpenCore Configuration

<img align="right" src="https://dl.exploitox.de/t480-oc/Hackintosh-T480-Sonoma.png" alt="macOS Sonoma running on the T480" width="425">

[![macOS](https://img.shields.io/badge/macOS-Monterey-brightgreen.svg)](https://developer.apple.com/documentation/macos-release-notes)
[![macOS](https://img.shields.io/badge/macOS-Ventura-brightgreen.svg)](https://developer.apple.com/documentation/macos-release-notes)
[![macOS](https://img.shields.io/badge/macOS-Sonoma-brightgreen.svg)](https://developer.apple.com/documentation/macos-release-notes)
[![OpenCore](https://img.shields.io/badge/OpenCore-0.9.3-blue)](https://github.com/acidanthera/OpenCorePkg)
[![License](https://img.shields.io/badge/license-MIT-purple)](/LICENSE)

<p align="center">
   <strong>Status: Maintained</strong>
   <br />
   <strong>Version: </strong>1.3.0
   <br />
   <a href="https://github.com/valnoxy/t480-oc/releases"><strong>Download now »</strong></a>
   <br />
   <a href="https://github.com/valnoxy/t480-oc/issues">Report Bug</a>
   ·
   <a href="https://github.com/valnoxy/t480-oc/blob/main/CHANGELOG.md">View Changelog</a>
   ·
   <a href="https://www.youtube.com/watch?v=thYDWyJuUq4">YouTube Video</a>
</p>
</p>
</br>

## ⚠️ Disclaimer
This guide is only for the Lenovo ThinkPad T480. I am NOT responsible for any harm you cause to your device. This guide is provided "as-is" and all steps taken are done at your own risk.

> The ACPI patches and the style of this README are from [EETagent](https://github.com/EETagent/T480-OpenCore-Hackintosh).

> **Important** macOS Sonoma no longer supports Broadcom Wifi cards. Long live Intel?

&nbsp;

## 💻 Tested devices
Some users have reported that similar ThinkPads are compatible with this OpenCore configuration. Here is a list of these devices:

- Lenovo ThinkPad T580
- [Lenovo ThinkPad X280](https://github.com/valnoxy/t480-oc/discussions/47)

&nbsp;

## Introduction

### EFI folders

This repo includes multiple EFI configurations for different macOS Versions.

| EFI               | Description                                                               | Type      |
| ----------------- | ------------------------------------------------------------------------- | --------- |
| `EFI`             | Supports macOS Monterey, Ventura & Sonoma (using Airportitlwm)            | `Stable`  |
| `EFI - HeliPort`  | Supports every macOS Version except Ventura, Require HeliPort app         | `Stable`  |

<a href="https://github.com/OpenIntelWireless/HeliPort/releases"><strong>
Download HeliPort app »</strong></a>

<details>
<summary><strong>💻 My Hardware</strong></summary>
...

&nbsp;

## Installation

<details>  
<summary><strong>📝 Requirements</strong></summary>
</br>

You must have the following items:
- Lenovo ThinkPad T480 (Obviously 😁).
- Access to a working Windows machine with Python installed.
- A pendrive with more than 4 GB (Remember that during the preparation we will format the flash drive to create the installation media).
- an Internet connection (recommended via Ethernet).
- 1-2 hours of your time.

...

</details>

<details>  
<summary><strong>⚙️ Preperation</strong></summary>
</br>

### Create the install media

First of all, you will need the install media of macOS. I will use [macrecovery](https://github.com/acidanthera/OpenCorePkg) to download and create the macOS Install media.

...

### Configure and install OpenCore
...

### GenSMBIOS
...

### Enter the proper ROM value
...

### ACPI patches
...

### Install OpenCore
...

</details>

<details>  
<summary><strong>🚚 Installation</strong></summary>
</br>

### Prepare BIOS
...

### Install macOS
...

</details>

...

## Post-install (optional)

<details>  
<summary><strong>💾 Install OpenCore to Hard drive</strong></summary>
</br>

1. Press `ALT + SPACE` and open terminal. Type `sudo diskutil mountDisk disk0s1` (where disk0s1 corresponds to the EFI partition of the main disk)
2. Open Finder and copy the EFI folder of your USB device to the main disk's EFI partition.
3. Unplug the USB device and reboot your laptop. Now you can boot macOS without your USB device.

</details>

<details>  
<summary><strong>✏️ Create a offline install media (Optional)</strong></summary>
</br>

In case of reinstalling macOS, a offline install media can save some time. You also don't need an Ethernet connection for the installation.
To create a offline install media, you need the following stuff: 

- macOS Installer from the App Store.
- A 16 GB pendrive (Keep in mind, during the preperation we will format the disk to create the install media).

...

</details>

...

## Status

<details>  
<summary><strong>✅ What's working</strong></summary>
</br>
 
- [X] Intel WiFi & Bluetooth (thanks to [itlwn](https://github.com/OpenIntelWireless/itlwm))
- [X] Brightness / Volume Control
- [X] Battery Information
- [X] Audio (Audio Jack & Speaker)
- [X] USB Ports & Built-in Camera
- [X] Graphics Acceleration
- [X] Trackpoint / Touchpad
- [X] Power management / Sleep
- [X] FaceTime / iMessage (iServices)
- [X] HDMI
- [X] Automatic OS updates
- [X] Handoff / Universal Clipboard
- [X] Sidecar (Cable) / AirPlay to Mac
- [X] SIP / FireVault 2
- [X] USB-C

...

</details>

<details>  
<summary><strong>⚠️ What's not working</
