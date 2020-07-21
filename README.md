# Hackintosh - Intel i9 10900k Z490 Vision G
OpenCore EFI for a 100% stable Intel i9 10900k + Z490 Vision G Hackintosh

**Latest working macOS**: 10.15.6

Complete hardware specs:
- i9 10900k OC to 5.1GHz
- Gigabyte Z490 Vision G
- Fractal Design Celsius S24 Black 
- Radeon RX 5700 XT 8 GB
- Fenvi T919
- 64GB RAM - 3200 MHz DDR4
- 500GB Kingston A2000 NVMe PCIe SSD (macOS Partition) + 00GB Kingston A2000 NVMe PCIe SSD (Windows Partition) + 1TB Samsung Evo 860 SATA SSD + other HDDs for storage (shared with Windows)

**SMBIOS**: iMacPro1,1

The system dual boots Windows 10

## Get it running
0. Make sure to update your BIOS, disable VT-d, disable CSM support and enable XHCI Hand-off (for Airdrop/Continuity/Sidecar)
1. Create an macOS Catalina 10.15.x USB-Installer Stick, install OpenCore and copy my EFI folder ([how?](https://github.com/SchmockLord/Hackintosh-Intel-i9-10900k-Gigabyte-Z490-Vision-D#installation-notes))
2. Generate a new serial number, motherboard id and SMUUID (make sure serial number is **invalid** in order to iMessage/Facetime to work) ([how?](https://hackintosh.gitbook.io/-r-hackintosh-vanilla-desktop-guide/config.plist-per-hardware/skylake#explanation-5) + [this tool](http://mackie100projects.altervista.org/download-clover-configurator/))
3. Boot the new macOS partition

## What works
- macOS Catalina and macOS Big Sur
- WiFi and Bluetooth + Airdrop + Sidecar + Continuity (OOB thanks to Fenvi T919)
- Audio
- HDMI/DP (OOB thanks to 5700 XT)
- All USB ports
- 2.5Gbit Ethernet
- Everything iCloud related (Drive, iMessage, Facetime, unlock with Apple Watch, etc)
- IGPU (must be enabled in BIOS and then in clover, i currently have it disabled but it works 100%)
- Temperature monitoring for everything except GPU (no 5700xt temp support in VirtualSMC)
- DRM content (Netflix, ATV+, Airplay 2 mirroring etc)
- Shutdown/Reboot/Update to newer macOS builds over time

## What doesn't work
- Sleep? Never got the chance to test it, my hackintosh is up 24/7

![alt text](https://i.imgur.com/H0MNPxt.jpg "neofetch")

## Kexts used:
- AppleALC (audio)
- Lilu + Whatevergreen (Audio helper, DRM support, GPU helper)
- VirtualSMC + addons (you cannot boot without this + temperature support)
- FakePCIID (there is no real Mac running a 10900k, we must fool the macOS to boot. this is how)
- FakePCIID_Intel_I225-V (ethernet)
- FakePCIID_Intel_HDMI_Audio (optional, support for audio via HDMI)

## Drivers used:
- OpenCanopy.efi (required by OpenCore)
- OpenRuntime.efi (required by OpenCore)
- HFSPlus (optional, make HFS drives discoverable in OpenCore bootloader if you want to use Mojave or older macOS versions)

## Thanks/Credits
- [SchmockLord](https://github.com/SchmockLord/Hackintosh-Intel-i9-10900k-Gigabyte-Z490-Vision-D)
- [samuel21119](https://github.com/samuel21119/Intel-i9-10900-Gigabyte-Z490-Vision-G-Hackintosh)
- tonymacx86
- insanelymac


**Fuck /r/Hackintosh for not allowing EFI sharing**
