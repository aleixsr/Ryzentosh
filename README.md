# Ryzentosh
OpenCore EFI for AMD Ryzen running OS X on Gigabyte B550i Aorus Pro AX

## Specification
| **Component** | **Model** |
| ------------- | --------- |
| CPU | AMD Ryzen 7 3700X (8-Core) |
| RAM | 32GB (2 x 16GB) DDR4 @3200MHz CL16 |
| Mobo | Gigabyte B550i Aorus Pro AX (BIOS: F12)|
| Graphics | Sapphire Pulse Radeon RX 580 8GB GDDR5 Lite (Polaris) |

**OpenCore version**: [0.8.3](https://github.com/acidanthera/opencorepkg/releases)

## Compatible macOS versions
 - Monterey (12.5.1)
 - Big Sur (11.6.8)
 - Mojave (10.14.6)

## What Works
 - Wi-Fi : Intel AX200
 - Bluetooth : Intel
 - Ethernet : 1 Gbps
 - HDMI/DisplayPort
 - Internal/External audio jacks
 - Sleep/Wake up

## Issues/Workarounds
- "Memory Modules Misconfigured" when OSX has booted : change SMBIOS from iMacPro 7,1 to iMacPro 1,1
- Low FPS on gaming:
	- Changing from "uXcCAAC4BgEHALoGAQcADx9AAA==" to "uXcCAAC4BgYGBroGBgYGDzAPCQ==" in "algrey - mtrr_update_action - fix PAT" section gives pretty much better performances, but sound crackling appears when using HDMI/DP audio... https://github.com/AMD-OSX/bugtracker/issues/5. So, enable only one of these Kernel patches:
		- Shaneee - mtrr_update_action - fix PAT [my default] : Full FPS on gaming but issues using HDMI/DP audio.
		- algrey - mtrr_update_action - fix PAT : Audio works fine but you'll get low FPS on gaming.
- Don't have volume control when using HDMI/DP : Use MonitorControl app

## How to use
  1. Make your USB installer with [**this guide**](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/)
  	sudo /Applications/Install\ macOS\ YOUR\ VERSION.app/Contents/Resources/createinstallmedia --volume /Volumes/USB --nointeraction
  2. Clone the repository and paste "BOOT" and "OC" directories into your's pendrive "EFI" folder
  3. Download [**GenSMBIOS**](https://github.com/corpnewt/GenSMBIOS) to generate unique SMBIOS information. Run it and follow all steps, as the model select **iMacPro1,1 5**.
  4. Boot it!  

**You CAN NOT use SMBIOS from this repository, it MUST be unique for every macOS installation**

## Steps
 - BIOS: Update to F12 version (later versions have issues with sleep)
 	- Save & Exit → Load Optimized Defaults
 	- Tweaker → Extreme Memory Profile (X.M.P) : Profile1
 	- Tweaker → Advanced CPU Settings → SVM Mode : Enabled (only if you need virtualization)
 	- Settings → Platform Power → Wake on LAN : Disabled
 	- Settings → IO Ports → USB Configuration → XHCI Hand-off : Enabled
  - Settings → IO Ports → Above 4G decoding : Enabled    ¡THIS ONE IS VERY IMPORTANT TO AVOID KERNEL PANIC AT BOOT!
  - Settings → IO Ports → Re-Size BAR Support : Auto
  - Settings → Miscellaneous → IOMMU : Disabled
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
 - [[Kext] Lilu v1.6.2](https://github.com/acidanthera/Lilu)
 - [[Kext] VirtualSMC v1.3.0](https://github.com/acidanthera/VirtualSMC)
 - [[Kext] WhateverGreen v1.6.1](https://github.com/acidanthera/WhateverGreen)
 - [[Kext] AMDRyzenCPUPowerManagement v0.7.1](https://github.com/trulyspinach/SMCAMDProcessor)
 - [[Kext] SMCAMDProcessor v1.0](https://github.com/trulyspinach/SMCAMDProcessor)
 - [[Kext] AppleALC v1.7.4](https://github.com/acidanthera/applealc)
 - [[Kext] LucyRTL8125Ethernet v1.1.0](https://github.com/Mieze/LucyRTL8125Ethernet)
 - [[Kext] AppleMCEReporterDisabler v1.0](https://github.com/acidanthera/bugtracker/files/3703498/AppleMCEReporterDisabler.kext.zip)
 - [[Kext] RestrictEvents v1.0.8](https://github.com/acidanthera/RestrictEvents)
 - [[Kext] AirportItlwm v2.2.0](https://github.com/OpenIntelWireless/itlwm)
 - [[Kext] IntelBluetoothFirmware v2.2.0](https://github.com/OpenIntelWireless/IntelBluetoothFirmware)
 - [[Kext] BlueToolFixup v2.6.3](https://github.com/acidanthera/BrcmPatchRAM)

 - [[Tool] gibMacOS](https://github.com/corpnewt/gibMacOS)
 - [[Tool] GenSMBIOS](https://github.com/corpnewt/GenSMBIOSGenSMBIOS)
 - [[Tool] ProperTree](https://github.com/corpnewt/ProperTreeProperTree)
 - [[Tool] octool](https://github.com/rusty-bits/octool)

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

