# Ryzentosh
OpenCore EFI for AMD Ryzen running OS X on Gigabyte B550i Aorus Pro AX (macOS 10.15)

## Specification
| **Component** | **Model** |
| ------------- | --------- |

**OpenCore version**: 0.6.2  

## Compatible macOS versions
 - Catalina (10.15.x)

## Issues
? - Partially-working virtualization (only VirtualBox & Parallels Dekstop 13.1.0 or below)
? - Not working 3.5mm Jack microphone (only USB/Bluetooth microphones)

## How to use
  1. Make your USB installer with [**this guide**](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/)
  2. Clone the repository and paste "BOOT" and "OC" directories into your's pendrive "EFI" folder
  3. Download [**GenSMBIOS**](https://github.com/corpnewt/GenSMBIOS) to generate unique SMBIOS information. Run it and select **Generate SMBIOS**, as the model select **iMacPro1,1**.
  4. Open config.plist with [**ProperTree**](https://github.com/corpnewt/ProperTree) and go to PlatformInfo > Generic. Set MLB (Board Serial), SystemSerialNumber (Serial) and SystemUUID (SmUUID) to generated values. Change ROM to your network card's MAC address without the `:` character. [**How to get MAC Address?**](https://www.wikihow.com/Find-the-MAC-Address-of-Your-Computer)
  5. Boot it!  

**You CAN NOT use SMBIOS from this repository, it MUST be unique for every macOS installation**

## Steps
 - USB: sudo /Applications/Install\ macOS\ Big\ Sur\ Beta.app/Contents/Resources/createinstallmedia  --volume /Volumes/USB --nointeraction
 - BIOS: Update to F10 version
 	Save & Exit → Load Optimized Defaults
 	Tweaker → Extreme Memory Profile (X.M.P) : Profile1
 	Settings → Platform Power → Wake on LAN : Disabled
 	Settings → USB Configuration → XHCI Hand-off : Enabled
 	Boot → Fast Boot : Disabled
 	Boot → CMS Support : Disabled
 	Boot → Secure Boot → Secure Boot : Disabled


# Hackitosh Apps

# MacOS Apps

