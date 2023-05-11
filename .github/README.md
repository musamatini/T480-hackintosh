# T480 Hackintosh
**Specific OpenCore configuration for Lenovo Thinkpad T480**

<img src="https://raw.githubusercontent.com/HBlanqueto/T480-hackintosh/main/.github/assets/T480.webp" alt="img" align="right" width="220px">

![GNU](https://img.shields.io/static/v1?style=for-the-badge&message=GNU+General+Public+License+3.0&color=A42E2B&logo=GNU&logoColor=FFFFFF&label=)
![Apple](https://img.shields.io/static/v1?style=for-the-badge&message=OpenCore+0.9.2&color=000000&logo=Apple&logoColor=FFFFFF&label=)
![Repo Size](https://img.shields.io/github/repo-size/HBlanqueto/T480-hackintosh?style=for-the-badge)
## Disclaimer ⚠️

These OpenCore settings are based in [pierpaolodimarzo's EFI](https://github.com/pierpaolodimarzo/ThinkPad-T480) and [valnoxy's README](https://github.com/valnoxy/t480-oc). All components and services are working, you could see [this list](https://github.com/pierpaolodimarzo/ThinkPad-T480/tree/main#-what-works) to make an idea about. My EFI only works for the hardware showed bellow, if you use other bluetooth, wireless, audio card, you'll have to add respective kext manually to make it work; use one of the repository I based in for reference.

## Hardware 💻

> **Note** 
>
> As you can see that I don't use **NVMeFix.kext** due Western Digital has oficial support in macOS.

| Category        | Name                                  |
| --------------- | ------------------------------------- |
| **SMBIOS**      | MacBookPro15,2                        |
| **CPU**         | i7-8650                               |
| **GPU**         | Intel UHD Graphics 620                |
| **Memory**      | 24G (8+16) DDR4 2400MHz               |
| **LAN**         | Intel Ethernet Connection I219-V      |
| **Wifi**        | Intel Wi-Fi AC 8265NGW                |
| **Audio**       | Realtek ALC256                        |
| **Bluetooth**   | Bluetooth 4.2                         |
| **Storage**     | Western Digital Blue SN570 1 Tb       |
| **Thunderbolt** | JHL6240 Thunderbolt 3 LP Alpine Ridge |

## BIOS ⚙️
Make sure to configure your BIOS options like this
-  `Security > Security Chip`: **Disabled**
-  `Memory Protection > Execution Prevention`: **Enabled**
-  `Virtualization > Intel Virtualization Technology`: **Enabled**
-  `Virtualization > Intel VT-d Feature`: **Enabled**
-  `Anti-Theft > Computrace -> Current Setting`: **Disabled**
-  `Secure Boot > Secure Boot`: **Disabled**
-  `Intel SGX -> Intel SGX Control`: **Disabled**
-  `Device Guard`: **Disabled**

StartUp Menu
-  `UEFI/Legacy Boot`: **UEFI Only**
-  `CSM Support`: **No**

USB Menu
-  `Always On USB`: **Disabled** -> It is necessary to extend the battery life

Thunderbolt Menu
-  `Thunderbolt BIOS Assist Mode`: **Disabled**
-  `Wake by Thunderbolt(TM) 3`: **Disabled**
-  `Security Level`: **No Security**
-  `Support in Pre Boot Environment > Thunderbolt(TM) device`: **Enabled**

## Preparing USB 🛠️
> **Note**
>
>Next steps will need any of these tools in order to generate or modify files, make sure to download and extrac them before start.

- **Python 3** (any version, I installed it from Microsoft Store)
- [**ProperTree**]()
- [**GenSMBIOS**](https://github.com/corpnewt/GenSMBIOS)
### OpenCore
1. Download [OpenCorePkg](https://github.com/acidanthera/OpenCorePkg) as a ZIP.
2. Extract the OpenCorePkg-master.zip file.
3. Open `cmd.exe` with Administrator privileges and change the directory to OpenCorePkg-master\Utilities\macrecovery.
4. Enter the following command to download macOS:
```sh
# macOS Monterey (12)
python macrecovery.py -b Mac-E43C1C25D4880AD6 -m 00000000000000000 download

# macOS Ventura (13)
python macrecovery.py -b Mac-7BA5B2D9E42DDD94 download
```

### Formating USB
1. Plug your USB device.
2. Open CMD with administrative permissions, type `diskpart`
3. Type `list disk` to see your disk id.
4. Select your pendrive by typing `select disk <diskid>`
5. Clean the pendrive and convert it to GPT. First, type `clean` and then `convert gpt`.
6. Create a new partition where we can put our files on. First, type `create partition primary`, then select the new partition with `select partition 1` and format it `format fs=fat32 quick`.
7. Finally, mount your pendrive by typing `assign`

### Folders
1. Create the folder `com.apple.recovery.boot` on the pendrive. Copy `OpenCorePkg-master\Utilities\macrecovery\BaseSystem.dmg` and `Basesystem.chunklist` into that folder.
2. Download and copy the `EFI` folder of this repository and paste it into your USB.
3. Make sure you have `com.apple.recovery.boot` and `EFI` folders with 

### SMBIOS
> **Note**
>
> During the process, confirm the serial given has support with [Apple verification the coverage of a device](https://checkcoverage.apple.com/)

1. Start GenSMBIOS.bat and use option `1` to download MacSerial.
2. Choose option `2`, to select the path of the config.plist file. It will be located in `EFI -> OC` folder.
3. Choose option `3`, and enter `MacBookPro15,2` as the machine type.
4. Press `Q` to quit. Your config now should contain the requied serials.

## Installation 🔌
> **Note**
>
> 1. If you plan to boot macOS without USB you'll need to create an EfI partition during these steps.
> 2. During installation, your computer may restart sometimes, keep calm and continue the process.

### Boot USB
- Make sure you have an Internet connection or use Ethernet.

1. Restart your computer and open Boot Menu during startup with `F12`
2. Choose your USB device and wait.
3. A Black Screen with Boot options must be showed, touch the space bar to display more options to boot and choose the `OC DEVEL (dmg)`, you could recognize it like a yellow gear.
4. A menu must be display, choose `Utility Disk`

### Partitions
1. Choose the device which you'll install the system and apply the option `erase`. Make sure to have this settings.
   - Name: 'Macintosh HD'
   - Format: APFS
   - Scheme: GUID Partition Map
> In **Name** option you could write whatever you like (e.g. 'Thinkintosh HD', 'Ventura',  'macOS Ventura'), make sure you wrote a name you liked the most due to cannot change it after install it in the bootloader.
2. Once format done, choose your storage again and select `Partitions` option.
3. Select the `+` and choose the option that says `Create partition`, then resize the new partition created to 512 mb.
   - Format: MS-DOS (fat)
> Do not select ExFat, it won't be possible to boot OC.
### Base system
1. Once you done, exit `Utility Disk` and choose `Install macOS...` or `Reinstall macOS...`
2. Acept terms and conditions, now it will show you your devices options to install the system.
3. Choose the one you named steps before.
4. Now wait until the installation, It may take 1 hour, more or less...
5. Once the installation finished, your computer could restart without any reason. Just boot into your USB again.
6. All is under control if you see in the bootloader option something with the name `macOS Installer`. Just select it and boot it.
7. During this time, the system could restart 2 times more or even 3, just insist booting the option told before.

## Enjoy the system 🎓
Congratulation, now you'll see `Select Your Country or Region` interface, that means the system is now installed in your computer.
> **Read troubleshooting** to know how to boot your EFI partition instead of USB.

<p align="center">
  <img src="https://raw.githubusercontent.com/HBlanqueto/T480-hackintosh/main/.github/assets/screenshot.png" alt="img" width="850px"/>
</p>

## Troubleshooting 🩺
### Samsung PM981
Most Thinkpad T480 has the `Samsung PM981` which is not compatible with macOS even using NVMeFIX.kext won´t works at all. [Reference](https://www.reddit.com/r/hackintosh/comments/evkljr/samsung_pm981_nvme_hackintosh_reboot_loop/).

### System language
The default keyboard layout and language is Spanish. The value for English would be `en-US:0`. Check this value language [list](https://github.com/acidanthera/OpenCorePkg/blob/master/Utilities/AppleKeyboardLayouts/AppleKeyboardLayouts.txt).

To change the language modify:
- `NVRAM -> Add -> 7C436110-AB2A-4BBB-A880-FE41995C9F82 -> prev-lang:kbd`

### Boot without USB
1. Open macOS' Terminal and type `sudo diskutil mountDisk disk0s1` (disk0s1 name could depend in the way you created the EFI partition use Utility Disk to check partition)
2. Open Finder and copy the `EFI` folder from the USB to the main disk's `EFI` partition.
3. Unplug the USB device and reboot your laptop. Now you can boot macOS without your USB device.

### BIOS entry
This is recommend for dualbooting more than one system in your computer. By default this is enabled in this configuration.
#### **Enable**
OC writes an entry into BIOS pointing directly to OpenCore.efi and the computer's boot menu shows OC and connected disks.
- `Misc > Boot > LauncherOption = Full`
- `Misc > Boot > LauncherPath = Default`
#### **Disable**
Computer's boot menu shows connected disks but OC does not write its own entry into BIOS
- `Misc > Boot > LauncherOption = Disabled`
- `Misc > Boot > LauncherPath = Default`
### Hide OpenCore
If you want to boot directly to macOS system, using [ProperTree](tool) you need to add this to your `config.plist`:
- `Misc > Boot > ShowPicker = False`
- `Misc > Boot > UsePicker = True`

### Hide EFI partitions
During the bootloader, EFI partitions may be showed. Hiding this is easiestGG as adding `.contentVisibility` file into **BOOT** and **OC** folders. By default this is enabled in this configuration.

## Special Greetings 🎉
- [Dortania Gudie](https://dortania.github.io/OpenCore-Install-Guide/)
- [pierpaolodimarzo](https://github.com/pierpaolodimarzo/ThinkPad-T480)
- [valnoxy](https://github.com/valnoxy/t480-oc)
