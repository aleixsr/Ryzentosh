# Ryzentosh
Hackintosh OpenCore EFI for AMD **Ryzen** running OS X on **Gigabyte B550i Aorus Pro AX**.

## Specification
| **Component** | **Model** |
| ------------- | --------- |
| CPU | AMD Ryzen 7 3700X (8-Core) |
| RAM | 32GB (2 x 16GB) DDR4 @3200MHz CL16 |
| Mobo | Gigabyte B550i Aorus Pro AX (rev 1.0) BIOS F17 |
| Graphics | Sapphire Pulse Radeon RX 6600 8GB GDDR6 (Navi 23) | Sapphire Pulse Radeon RX 580 8GB GDDR5 Lite (Polaris) |

**OpenCore version**: [0.9.4](https://github.com/acidanthera/opencorepkg/releases)

## Compatible macOS versions
 - Monterey (12.7.4)

## What Works
 - Wi-Fi : Intel AX200
 - Bluetooth : Intel AX200
 - Ethernet : 1 Gbps
 - HDMI/DisplayPort
 - Internal/External audio jacks
 - Sleep/Wake up (fixed on any BIOS now!)

<a href="https://www.buymeacoffee.com/aleixsr" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-blue.png" alt="Buy Me A Coffee" style="height: 60px !important;width: 217px !important;" ></a>

## Issues/Workarounds
- "Memory Modules Misconfigured" when OSX has booted : change SMBIOS from iMacPro 7,1 to iMacPro 1,1.
- Low FPS on gaming:
	- Changing from "uXcCAAC4BgEHALoGAQcADx9AAA==" to "uXcCAAC4BgYGBroGBgYGDzAPCQ==" in "algrey - mtrr_update_action - fix PAT" section gives pretty much better performances, but sound crackling appears when using HDMI/DP audio... https://github.com/AMD-OSX/bugtracker/issues/5. So, enable only one of these Kernel patches:
		- Shaneee - mtrr_update_action - fix PAT [my default] : Full FPS on gaming but issues using HDMI/DP audio.
		- algrey - mtrr_update_action - fix PAT : Audio works fine but you'll get low FPS on gaming.
- Don't have volume control when using HDMI/DP : Use MonitorControl app.

## How to use
  1. Make your USB installer with [**this guide**](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/)
  	sudo /Applications/Install\ macOS\ YOUR\ VERSION.app/Contents/Resources/createinstallmedia --volume /Volumes/USB --nointeraction
  2. Clone the repository and paste "BOOT" and "OC" directories into your's pendrive "EFI" folder
  3. Download [**GenSMBIOS**](https://github.com/corpnewt/GenSMBIOS) to generate unique SMBIOS information. Run it and follow all steps, as the model select **iMacPro1,1 5**.
  4. Boot it!  

**You CAN NOT use SMBIOS from this repository, it MUST be unique for every macOS installation**

## BIOS
 - ~~Update to F12 version (later versions have issues with sleep)~~ Update to F17.
 - Save & Exit → Load Optimized Defaults
 - Tweaker → Extreme Memory Profile (X.M.P) : Profile1
 - Tweaker → Advanced CPU Settings → SVM Mode : Enabled (only if you need virtualization)
 - ~~Settings → Platform Power → Wake on LAN : Disabled~~
 - ~~Settings → IO Ports → USB Configuration → XHCI Hand-off : Enabled~~
 - Settings → IO Ports → Above 4G decoding : Enabled    ¡THIS ONE IS VERY IMPORTANT TO AVOID KERNEL PANIC AT BOOT!
 - Settings → IO Ports → Re-Size BAR Support : Auto
 - ~~Settings → Miscellaneous → IOMMU : Auto~~
 - Boot → Fast Boot : Disabled
 - Boot → CMS Support : Disabled
 - Boot → Secure Boot → Secure Boot : Disabled
 		
## Post Installation
- Move your OpenCore EFI folder to a MacOS drive: https://dortania.github.io/OpenCore-Post-Install/universal/oc2hdd.html#grabbing-opencore-off-the-usb

## Hints
- To disable SIP enter in recovery mode an run "csrutil disable" in terminal.
- If you've dual boot:
	- To enable macOS-only SMBIOS injection:
		- Kernel → Quirks → CustomSMBIOSGuid → True
		- Platforminfo → CustomSMBIOSMode → Custom
	- To have UTC clock and fix Windows 10 issues : DualBoot/UniversalTimeFix.reg
	- Disable Fast Boot on Windows 10 : DualBoot/DisableFastBoot.reg
	- NTFS r/w support : brew install ntfs-3g; brew cask install mounty

## Credits
 - [[Kext] Lilu](https://github.com/acidanthera/Lilu) :: Hackintosh patching tool.
 - [[Kext] VirtualSMC](https://github.com/acidanthera/VirtualSMC) :: Hackintosh system management controller (thermal management and power supply, battery charging, video mode switching, sleep and wake, hibernation, and LED indicators).
 - [[Kext] WhateverGreen](https://github.com/acidanthera/WhateverGreen) :: [Lilu plugin] GPU patching.
 - [[Kext] NootRX](https://github.com/ChefKissInc/NootRX) :: [Lilu plug-in for unsupported RDNA 2 dGPUs] GPU patching.
 - [[Kext] RestrictEvents](https://github.com/acidanthera/RestrictEvents) :: Prevents compatibility issues.
 - [[Kext] AppleALC](https://github.com/acidanthera/applealc) :: Audio driver.
 - [[Kext] AMDRyzenCPUPowerManagement](https://github.com/trulyspinach/SMCAMDProcessor) :: Power management and monitoring for AMD processors.
 - [[Kext] SMCAMDProcessor v1.0](https://github.com/trulyspinach/SMCAMDProcessor) :: [Requires AMDRyzenCPUPowerManagement] Publish power management and monitoring for AMD processors.
 - [[Kext] AGPMInjector](https://github.com/aluveitie/AGPMInjector) :: GPU power management.
 - [[Kext] SMCRadeonGPU/RadeonSensor](https://github.com/NootInc/RadeonSensor) :: Temperature sensor for AMD GPUs.
 - [[Kext] LucyRTL8125Ethernet](https://github.com/Mieze/LucyRTL8125Ethernet) :: Realtek RTL8125 2.5GBit Ethernet driver.
 - [[Kext] USB ToolBox/UTBMap-all-headers and UTBMap-no-headers v1.1.1](https://github.com/USBToolBox/kext) :: Mobo USB mapping (enable only 1 of these 2 headers).
 - [[Kext] AppleMCEReporterDisabler](https://github.com/acidanthera/bugtracker/files/3703498/AppleMCEReporterDisabler.kext.zip) :: Required on AMD systems (Affected SMBIOSes: MacPro6,1 MacPro7,1 iMacPro1,1).
 - [[Kext] AirportItlwm](https://github.com/OpenIntelWireless/itlwm) :: Intel Wi-Fi driver.
 - [[Kext] IntelBluetoothFirmware/IntelBTPatcher/IntelBluetoothInjector v2.3.0](https://github.com/OpenIntelWireless/IntelBluetoothFirmware) :: Intel BlueTooth driver.
 - [[Kext] BlueToolFixup](https://github.com/acidanthera/BrcmPatchRAM) :: BlueTooth patcher required for macOS 12 or newer.
 - [[Kext] NVMeFix](https://github.com/acidanthera/NVMeFix) :: Patches for the Apple NVMe storage driver, IONVMeFamily. Its goal is to improve compatibility with non-Apple SSDs.

 - [[Tool] gibMacOS](https://github.com/corpnewt/gibMacOS) :: Download macOS versions via CLI.
 - [[Tool] GenSMBIOS](https://github.com/corpnewt/GenSMBIOSGenSMBIOS) :: Generate custom SMBIOS.
 - [[Tool] ProperTree](https://github.com/corpnewt/ProperTreeProperTree) :: Edit plist files easly.
 - [[Tool] octool](https://github.com/rusty-bits/octool) :: Tool that helps creating your custom EFI.

 - [[Repo] radianttap/EFI-B550I-Aorus](https://github.com/radianttap/EFI-B550I-Aorus)
 - [[Repo] mikigal/ryzen-hackintosh](https://github.com/mikigal/ryzen-hackintosh)

 <br><br> Many thanks to all the help from AMD-OS X Forums.


# Hackitosh Apps
- Install Homebrew : 
	- /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
- Karabiner :
	- brew install --cask karabiner-elements
	- Import settings from karabiner/ folder
	- If doesn't work change keyboard to "virtual" and cahnge to USB Keyboard again
- Hackintool : brew install --cask hackintool
- OpenCore Configurator : brew install --cask opencore-configurator


# MacOS Apps
- iTerm2 + Oh My Zsh! :
	- brew install --cask iterm2
	- brew install zsh zsh-completions
	- Follow https://www.freecodecamp.org/news/how-to-configure-your-macos-terminal-with-zsh-like-a-pro-c0ab3f3c1156/
- XtraFinder : https://www.trankynam.com/xtrafinder/
- HyperSwitch : brew install --cask hyperswitch
- Maccy : brew install --cask maccy
- Caffeine : brew install --cask caffeine
- iStat Menus : brew install --cask istat-menus
- Keka : brew install --cask keka
- Shottr Screenshot : brew install --cask shottr
- MonitorControl : brew install --cask monitorcontrol
- Numi : brew install --cask numi
- PingMenu : brew install --cask pingmenu
- Tunnelblick : brew install --cask tunnelblick
- Sublime Text : brew install --cask sublime-text

# Bonus Track
- Disable cration of junk files (._)
  - defaults write com.apple.desktopservices DSDontWriteUSBStores -bool true
  - defaults write com.apple.desktopservices DSDontWriteNetworkStores -bool true

