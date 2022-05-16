<img src="https://i.imgur.com/foW4AcU.jpg" height="350" title="HackintoshLogo">

# macOS Monteray - Hackintosh

**Latest working macOS**: 12.3.1

**Current OpenCore**: 0.8.0

Complete hardware specs:
- **CPU**: Intel 10900k OC to 5.1GHz
	- **Cooling**: 
		- Noctua NH-D15 (with Thermal Grizzly Kryonaut) 
		- 6x Noctua Fans around the case for airflow
- **Motherboard**: Gigabyte Z490 Vision G
- **GPU**: AMD Radeon RX 6900 XT
- **WiFi/Bluetooth**: Fenvi T919 with wired antennas
- **Ethernet**: Realtek RTL8125B PCI Express 2.5 Gigabit Ethernet
- **RAM**: 64GB @ 3200 MHz DDR4
- **NVME SSD**: 
	- 500GB Kingston A2000 NVMe PCIe SSD (macOS)
	- 500GB Kingston A2000 NVMe PCIe SSD (Windows)
- **SATA SSD**: 
	- 4TB Samsung Evo 860 SATA SSD (shared with Windows and Linux, formatted as exFAT)
	- 500GB Samsung Evo 840 SATA SSD (Linux)
- **PC Case**: NZXT H710 (important because front usb ports are mapped)

**SMBIOS**: iMac20,2

The system triple boots Windows 11 and Linux Mint

## Tools
- [OpenCore Auxiliary Tools](https://github.com/ic005k/QtOpenCoreConfig) - easy `config.plist` management
	- [OpenCore Configurator](https://mackie100projects.altervista.org/download-opencore-configurator/) - alternative for OCAT
- [Hackintool](https://github.com/headkaze/Hackintool/releases) - debug and map USB ports

## Get it running
1. Make sure to update your BIOS, disable CSM support and enable XHCI Hand-off (for Airdrop/Continuity/Sidecar)
2. Create an macOS Monteray/Big Sur USB-Installer Stick, install OpenCore and copy my EFI folder ([how?](https://github.com/SchmockLord/Hackintosh-Intel-i9-10900k-Gigabyte-Z490-Vision-D#installation-notes))
3. Generate a new serial number, motherboard id, ROM (that's your motherboard's mac address without dots) and SMUUID (make sure serial number is **invalid** in order to iMessage/Facetime to work) ([how?](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#platforminfo))
4. Boot the new macOS partition

## What works
- macOS Monteray (12.3.1) and Big Sur (11.6.1)
- WiFi and Bluetooth + Airdrop + Sidecar + Continuity (OOB via Fenvi T919)
- Audio
- HDMI/DP (with VRR)
- All USB ports
- Everything iCloud related (Drive, iMessage, Facetime, unlock with Apple Watch, etc)
- Intel Quick Sync (if you enable iGPU in BIOS)
- Temperature monitoring
- Resizable Bar Support (enable Above 4G Decoding in BIOS)
- Shutdown/Reboot/Update to newer macOS builds over time

## What doesn't work
- I225-V 2.5Gbit Ethernet Adapter on Monteray only works if you [reflash the firmware](https://github.com/5T33Z0/Gigabyte-Z490-Vision-G-Hackintosh-OpenCore/blob/main/I225-V_FIX.md).

I'm currently using a PCI card (Realtek RTL8125B PCI Express 2.5 Gigabit Ethernet) with the LucyRTL8125Ethernet kext as I already bought the card before the fix was found.

## Not tested
- Sleep

## Port mapping
All USB ports work **except** the two next to the ethernet port (HS03/SS03 and HS04/SS04). I needed another USBC port on the front of my case + a USB 3 port + a USB 2 port so i had to disable those 2. If you don't need front IO (or use a different PC case) you can use `USBInjectAll.kext`, set `XhciPortLimit = true` and use Hackintool to map the ports you want.
The USBC port on the motherboard works and it's reversible.

![usb mapping](https://i.imgur.com/MlT8SOk.png "usb mapping")

## Kexts used:
- Lilu
- Whatevergreen
- AppleALC (audio layout 28)
- VirtualSMC + SMCProcessor + SMCSuperIO
- USBPorts
- LucyRTL8125Ethernet (optional)

## Drivers used:
- OpenCanopy
- OpenRuntime
- OpenLinuxBoot (optional)
- OpenHfsPlus (optional)

![neofetch](https://i.imgur.com/Y3nMbr4.png)

## Thanks/Credits
- [5T33Z0](https://github.com/5T33Z0/Gigabyte-Z490-Vision-G-Hackintosh-OpenCore)
- [SchmockLord](https://github.com/SchmockLord/Hackintosh-Intel-i9-10900k-Gigabyte-Z490-Vision-D)
- [samuel21119](https://github.com/samuel21119/Intel-i9-10900-Gigabyte-Z490-Vision-G-Hackintosh)
- tonymacx86
- insanelymac


**Fuck /r/Hackintosh mods for not allowing EFI sharing and being on power trips**
