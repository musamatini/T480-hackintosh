# Thinkpad T480 Hackintosh 🍏
Welcome to the T480 Hackintosh project, aimed at enabling macOS to run on the Lenovo Thinkpad T480. 🚀
<br/><br/>
<br/><br/>
<img src="https://raw.githubusercontent.com/musamatini/T480-hackintosh/main/.github/assets/ThinkpadT480.png" alt="img" align="right" width="220px">

## Disclaimer ⚠️

This EFI is built upon the foundations of the [pierpaolodimarzo](https://github.com/pierpaolodimarzo/ThinkPad-T480) and [valnoxy](https://github.com/valnoxy/t480-oc) repositories. Credit goes to them for their valuable work.

Please refer to their repositories for more information and consider supporting their efforts.


## Hardware Specifications 🛠️

> IMPORTANT!
>
> 1. Add **NVMeFix.kext** if you don't use any Western Digital storage device.
> 2. Generate your own **SMBIOS** or your won't be able to use Apple Services.

| Category       | Details                            |
| -------------- | ---------------------------------- |
| Display        | 1920x1080                          |
| SMBIOS         | MacBookPro15,2                     |
| CPU            | Intel Core i7-8650                 |
| GPU            | Intel UHD Graphics 620             |
| Memory         | 64GB (32x2) DDR4 3200MHz           |
| LAN            | Intel Ethernet Connection I219-V   |
| Wifi           | Intel Wi-Fi AC 8265NGW             |
| Audio          | Realtek ALC256                     |
| Bluetooth      | Bluetooth 4.2                      |
| Storage        | Western Digital Blue SN570 1TB     |
| Thunderbolt    | JHL6240 Thunderbolt 3 LP Alpine Ridge |

## BIOS Configuration 🔧

For successful installation, configure your BIOS settings as follows:

- Security > Security Chip: **Disabled**
- Memory Protection > Execution Prevention: **Enabled**
- Virtualization > Intel Virtualization Technology: **Enabled**
- Virtualization > Intel VT-d Feature: **Enabled**
- Anti-Theft > Computrace > Current Setting: **Disabled**
- Secure Boot > Secure Boot: **Disabled**
- Intel SGX Intel SGX Control: **Disabled**
- Device Guard: **Disabled**

Make sure to set your StartUp Menu options to UEFI Only and disable `CSM Support`.

For USB settings, set `Always On USB` to **Disabled**.

In the Thunderbolt Menu, configure the settings accordingly.

## Preparing USB ⚙️

Before installation, ensure you have the following tools:

- [**Python 3**](https://www.python.org/)
- [**ProperTree**](https://github.com/corpnewt/ProperTree)
- [**GenSMBIOS**](https://github.com/corpnewt/GenSMBIOS)

Follow these steps to prepare your USB:

1. Format the USB using the provided commands in CMD with administrative permissions.
2. Download macOS with the provided commands in Windows Terminal or CMD.
3. Create and organize necessary folders and files in the USB.
4. Download the `EFI` folder from the repository and copy it to the USB.

- [EFI Installation](#efi-installation) 🖥️

- Boot from your prepared USB device.
- Choose the OC DEVEL (dmg) option from the boot menu.
- Perform the required disk management steps for installation.
- Follow the installation process and wait for the system to be installed.
- Reboot your laptop and proceed with the remaining setup steps.

## Booting without USB 🚀

- Mount the EFI partition of your main disk.
- Copy the EFI folder from the USB to the main disk's EFI partition.
- Unplug the USB device and reboot your laptop to boot macOS.

## Troubleshooting 🛠️❗

For any troubleshooting or customization needs, please refer to the [Troubleshooting](#troubleshooting) section of the repository.

## Special Thanks 🙌

A big thank you to the following references and projects that made this hackintosh project possible:

- [Dortania Guide](https://dortania.github.io/OpenCore-Install-Guide/)
- [pierpaolodimarzo](https://github.com/pierpaolodimarzo/ThinkPad-T480)
- [valnoxy](https://github.com/valnoxy/t480-oc)

Your support and contribution are greatly appreciated! 👏
