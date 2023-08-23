# Thinkpad T480 Hackintosh 🍏
Welcome to the T480 Hackintosh project, aimed at enabling macOS to run on the Lenovo Thinkpad T480. 🚀
<br/><br/>

<img src="https://raw.githubusercontent.com/musamatini/T480-hackintosh/main/.github/assets/ThinkpadT480.png" alt="img" align="right" width="220px">

## Disclaimer ⚠️

This EFI is based in [pierpaolodimarzo](https://github.com/pierpaolodimarzo/ThinkPad-T480) and [valnoxy](https://github.com/valnoxy/t480-oc) repository, go and support them. This repository couldn't be done without their work.

I constantly check `config.plist`status with [sanitychecker](https://sanitychecker.ocutils.me/results/6d99f7fc-bb02-4f1b-8e30-99600eefad79), I'll recommends you to use It as the tool in the OpenCore-PKG, any suggestion is acepted to improve the files.

**What's working?**

Most of all components and services are working, take a look to [pierpaolodimarzo's list](https://github.com/pierpaolodimarzo/ThinkPad-T480/tree/main#-what-works) to make an idea about.

<br/>

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

<br/>

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


<br/>

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

<br/>

## EFI Installation🖥️

- Boot from your prepared USB device.
- Choose the OC DEVEL (dmg) option from the boot menu.
- Perform the required disk management steps for installation.
- Follow the installation process and wait for the system to be installed.
- Reboot your laptop and proceed with the remaining setup steps.

<br/><br/>

## Booting without USB 🚀

- Mount the EFI partition of your main disk.
- Copy the EFI folder from the USB to the main disk's EFI partition.
- Unplug the USB device and reboot your laptop to boot macOS.
  
<br/>

## Troubleshooting 🩺
> [ProperTree](https://github.com/corpnewt/ProperTree) is going to be used for modifying `config.plist`. Remember to install `hombrew` and `python-tk` dependency, also you can build te app in macOS.


### Customize OpenCore
Dortania's guide has a section that shows many [themes](https://dortania.github.io/OpenCanopy-Gallery/blackosx.html#themes) made by blackosx. In GitHub there are other OpenCore themes not showed in the guide but you could inquire them.

### Samsung PM981
Most Thinkpad T480 has the `Samsung PM981` which is not compatible with macOS even using NVMeFIX.kext won´t works at all. [Reference](https://www.reddit.com/r/hackintosh/comments/evkljr/samsung_pm981_nvme_hackintosh_reboot_loop/).

### System language
The default keyboard layout and language is Spanish. The value for English would be `en-US:0`. Check this value language [list](https://github.com/acidanthera/OpenCorePkg/blob/master/Utilities/AppleKeyboardLayouts/AppleKeyboardLayouts.txt).

To change the language modify:
- `NVRAM > Add > 7C436110-AB2A-4BBB-A880-FE41995C9F82 > prev-lang:kbd`

### Latam keyboard
My keyboard has some troubles in the hackintosh, I have the "<>" keys at the bottom of the keyboard, this repository has fixed that key. Follow its README to install.

- [Latam-keyboard by neosergio](https://github.com/neosergio/Latam-Keyboard)

### BIOS entry
By default this is enabled in this `config.plist`. I'll recommend this by default.
#### Enable
OC writes an entry into BIOS pointing directly to OpenCore.efi and the computer's boot menu shows OC and connected disks.
- `Misc > Boot > LauncherOption = Full`
- `Misc > Boot > LauncherPath = Default`
#### Disable
Computer's boot menu shows connected disks but OC does not write its own entry into BIOS
- `Misc > Boot > LauncherOption = Disabled`
- `Misc > Boot > LauncherPath = Default`

### Hide OpenCore
In the `config.plist` modify next line to show or hide the Boot Menu, I personally do not recommend this due to some cases a macOS update could break something.
- `Misc > Boot > ShowPicker = False`
- `Misc > Boot > UsePicker = True`

### Change OpenCore background color
We have to modify with hex valor the backgrounds color. Modify and change the value with the color you want (e.g. BFBFBF)
- `NVRAM > Add > 4D1EDE05-38C7-4A6A-9CC6-4BCCA8B38C14 > DefaultBackgroundColor > <000000>`

### Change NVRAM size
By default It is recommend to use 1.5Gb, even macbook Pro use the same size, but If you are who likes to using more, read next Reddit post about It.

- [Whatevergreen iGPU VRAM allocation via framebuffer-unifiedmem](https://www.reddit.com/r/hackintosh/comments/gp07ko/whatevergreen_igpu_vram_allocation_via/?utm_source=share&utm_medium=android_app&utm_name=androidcss&utm_term=1&utm_content=2)

### Hide EFI partitions
During the bootloader, EFI partitions may be showed. Hiding this is easiest as adding `.contentVisibility` file into **BOOT** and **OC** folders. By default this is enabled in this configuration.

### Disable smoothing font
Smoothing font can exhaust the eyes in 1366x768 display, disable It with next command.
```sh
# disable font smoothing
defaults -currentHost write -g AppleFontSmoothing -int 0

# enable default smoothing. You can also use "1" for light smoothing and "3" value for strong smoothing.
defaults -currentHost write -g AppleFontSmoothing -int 2
```

<br/>

## Special Thanks 🙌

A big thank you to the following references and projects that made this hackintosh project possible:

- [Dortania Guide](https://dortania.github.io/OpenCore-Install-Guide/)
- [pierpaolodimarzo](https://github.com/pierpaolodimarzo/ThinkPad-T480)
- [valnoxy](https://github.com/valnoxy/t480-oc)

Your support and contribution are greatly appreciated! 👏
