# macOS Monteray - Hackintosh

**Latest working macOS**: 12.1

**Current OpenCore**: 0.7.6

Complete hardware specs:
- **CPU**: Intel 10900k OC to 5.1GHz
	- **Cooling**: Noctua NH-D15 (with Thermal Grizzly Kryonaut) 
- **Motherboard**: Gigabyte Z490 Vision G
- **GPU**: AMD Radeon RX 6900 XT
- **WiFi/Bluetooth**: Fenvi T919
- **RAM**: 64GB @ 3200 MHz DDR4
- **NVME SSD**: 
	- 500GB Kingston A2000 NVMe PCIe SSD (macOS Partition)
	- 500GB Kingston A2000 NVMe PCIe SSD (Windows Partition)
- **SATA SSD**: 4TB Samsung Evo 860 SATA SSD (shared with Windows, formatted as exFAT)
- **PC Case**: NZXT H710 (important because front usb ports are mapped)

**SMBIOS**: iMac20,2

The system dual boots Windows 11

## Tools
- [OpenCore Auxiliary Tools](https://github.com/ic005k/QtOpenCoreConfig) - easy `config.plist` management
	- [OpenCore Configurator](https://mackie100projects.altervista.org/download-opencore-configurator/) - alternative for OCAT
- [Hackintool](https://github.com/headkaze/Hackintool/releases) - debug and map USB ports

## Get it running
1. Make sure to update your BIOS, disable CSM support and enable XHCI Hand-off (for Airdrop/Continuity/Sidecar)
2. Create an macOS Big Sur/Monteray USB-Installer Stick, install OpenCore and copy my EFI folder ([how?](https://github.com/SchmockLord/Hackintosh-Intel-i9-10900k-Gigabyte-Z490-Vision-D#installation-notes))
3. Generate a new serial number, motherboard id, ROM (that's your motherboard's mac address without dots) and SMUUID (make sure serial number is **invalid** in order to iMessage/Facetime to work) ([how?](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#platforminfo))
4. Boot the new macOS partition

## What works
- macOS Monteray (12.1) and Big Sur (11.6.1)
- WiFi and Bluetooth + Airdrop + Sidecar + Continuity (OOB via Fenvi T919)
- Audio
- HDMI/DP (Variable Refresh Rate if your Display is FreeSync 2 compatible)
- All USB ports
- Everything iCloud related (Drive, iMessage, Facetime, unlock with Apple Watch, etc)
- Intel Quick Sync (if you enable iGPU in BIOS)
- Temperature monitoring for everything except GPU (no GPU temp support in VirtualSMC for navi and big navi cards)
- Resizable Bar Support (enable Above 4G Decoding in BIOS)
- Shutdown/Reboot/Update to newer macOS builds over time

## What doesn't work
I225-V 2.5Gbit Ethernet Adapter on Monteray (worked on Big Sur with a bootarg still present in the `config.plist`).
I'm currently using a generic gigabit USB dongle until this gets fixed. [Here](https://www.insanelymac.com/forum/topic/348493-discussion-intel-i225-v-on-macos-monterey/) and [here](https://github.com/dortania/bugtracker/issues/213#issuecomment-927155047) are some interesting threads with people trying to make it play nice on Monteray.

## Port mapping
All USB ports work **except** the two next to the ethernet port (HS03/SS03 and HS04/SS04). I needed another USBC port on the front of my case + a USB 3 port + USB 2 port so i had to disable those 2. If you don't need front IO (or use a different PC case) you can use `USBInjectAll.kext`, set `XhciPortLimit = true` and use Hackintool to map the ports you want.
The USBC port on the motherboard works and it's reversible.

![alt text](https://i.imgur.com/MlT8SOk.png "usb mapping")

## Kexts used:
- Lilu
- Whatevergreen
- AppleALC (audio layout 28)
- VirtualSMC + SMCProcessor + SMCSuperIO
- USBPorts

## Neofetch
![alt text](https://i.imgur.com/jBZFQJN.jpg "neofetch")

## Drivers used:
- OpenCanopy
- OpenRuntime
- OpenLinuxBoot (optional)
- OpenHfsPlus (optional)

## Thanks/Credits
- [5T33Z0](https://github.com/5T33Z0/Gigabyte-Z490-Vision-G-Hackintosh-OpenCore)
- [SchmockLord](https://github.com/SchmockLord/Hackintosh-Intel-i9-10900k-Gigabyte-Z490-Vision-D)
- [samuel21119](https://github.com/samuel21119/Intel-i9-10900-Gigabyte-Z490-Vision-G-Hackintosh)
- tonymacx86
- insanelymac


**Fuck /r/Hackintosh mods for not allowing EFI sharing and being on power trips**
