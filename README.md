# Ryzentosh
OpenCore EFI for AMD Ryzen running OS X on Gigabyte B550i Aorus Pro AX

## Specification
| **Component** | **Model** |
| ------------- | --------- |
| CPU | AMD Ryzen 7 3700X |
| RAM | 32GB (2 x 16GB) DDR4 @3200MHz CL16 |
| Mobo | Gygabyte B550i Aorus Pro AX |
| Graphics | Sapphire Pulse Radeon RX 580 8GB GDDR5 Lite |

**OpenCore version**: [0.6.4](https://github.com/acidanthera/opencorepkg/releases)

## Compatible macOS versions
 - Mojave (10.14.x)
 - Catalina (10.15.x) : Sleep not working (cannot wake up from sleep)
 - Big Sur (11.0.1, 11.1)

## What Works
 - Wi-Fi : Intel AX200 (see workaround)
 - Bluetooth
 - Ethernet : 1 Gbps (see workaround)
 - HDMI/DisplayPort
 - Internal/External audio jacks
 - Sleep/Wake up

## Issues/Workarounds
- Intel Wi-Fi : Run Tools/HeliPort app at login, please check [FAQs] https://openintelwireless.github.io/itlwm/FAQ.html
- LAN-Fix-Realtek® 2.5GbE LAN : Not Connected
	- System Preferences → Network → Select your Ethernet controller. Normally it says (not connected)  → Advanced → Hardware:
		- Switch from Automatically to Manually
		- Speed : 1000baseT (if doesn't work 100baseTX
		- Duplex : full-duplex, flow-control, energy-efficient-ethernet
		- MTU : Standard (1500)
	- Command Line option : "sudo ifconfig en0 media 1000baseT mediaopt full-duplex"
- "Memory Modules Misconfigurured" when OSX has booted : change SMBIOS from iMacPro 7,1 to iMacPro 1,1
- Low FPS on gaming:
	- Changing from "uXcCAAC4BgEHALoGAQcADx9AAA==" to "uXcCAAC4BgYGBroGBgYGDzAPCQ==" in "algrey - mtrr_update_action - fix PAT" section gives pretty much better performances, but sound crackling appears when using HDMI/DP audio... https://github.com/AMD-OSX/bugtracker/issues/5
	- config.plist : Full FPS on gaming but issues using HDMI/DP audio.
	- config.plist.audioOK : Audio works fine but you'll get low FPS on gaming.
- Don't have volume control when using HDM/DP : Use MonitorControl app

## How to use
  1. Make your USB installer with [**this guide**](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/)
  	sudo /Applications/Install\ macOS\ YOUR\ VERSION.app/Contents/Resources/createinstallmedia --volume /Volumes/USB --nointeraction
  2. Clone the repository and paste "BOOT" and "OC" directories into your's pendrive "EFI" folder
  3. Download [**GenSMBIOS**](https://github.com/corpnewt/GenSMBIOS) to generate unique SMBIOS information. Run it and follow all steps, as the model select **iMacPro1,1 5**.
  4. Boot it!  

**You CAN NOT use SMBIOS from this repository, it MUST be unique for every macOS installation**

## Steps
 - BIOS: Update to F10 version
 	- Save & Exit → Load Optimized Defaults
 	- Tweaker → Extreme Memory Profile (X.M.P) : Profile1
 	- Tweaker → Advanced CPU Settings → SVM Mode : Enabled (only if you need virtualization)
 	- Settings → Platform Power → Wake on LAN : Disabled
 	- Settings → IO Ports → USB Configuration → XHCI Hand-off : Enabled
 	- Settings → AMD CBS → FCH Common Options → I2C Configuration Options → I2C 2 Enable : Disabled
 	- Settings → AMD CBS → FCH Common Options → I2C Configuration Options → I2C 3 Enable : Disabled
	- Settings → AMD CBS → FCH Common Options → ESPI Configuration Options → ESPI Enable : Disabled
 	- Boot → Fast Boot : Disabled
 	- Boot → CMS Support : Disabled
 	- Boot → Secure Boot → Secure Boot : Disabled
 		
## Post Installation
- Move your OpenCore EFI folder to a MacOS drive: https://dortania.github.io/OpenCore-Post-Install/universal/oc2hdd.html#grabbing-opencore-off-the-usb

## Hints
- SIP has been disabled permanently : csr-active-config = FF070000
- If you've dual boot:
	- To enable macOS-only SMBIOS injection:
		- Kernel → Quirks → CustomSMBIOSGuid → True
		- Platforminfo → CustomSMBIOSMode → Custom
	- To have UTC clock and fix Windows 10 issues : DualBoot/UniversalTimeFix.reg
	- Disable Fast Boot on Windows 10 : DualBoot/DisableFastBoot.reg
	- NTFS r/w support : brew install ntfs-3g; brew cask install mounty

## Credits
 - [[Kext] Lilu v1.5.0](https://github.com/acidanthera/Lilu)
 - [[Kext] VirtualSMC v1.1.9](https://github.com/acidanthera/VirtualSMC)
 - [[Kext] WhateverGreen v1.4.5](https://github.com/acidanthera/WhateverGreen)
 - [[Kext] AppleALC v1.5.5](https://github.com/acidanthera/AppleALC)
 - [[Kext] LucyRTL8125Ethernet v1.0.0](https://github.com/Mieze/LucyRTL8125Ethernet)
 - [[Kext] AMDRyzenCPUPowerManagement v0.6.6](https://github.com/trulyspinach/SMCAMDProcessor)
 - [[Kext] SMCAMDProcessor v1.0](https://github.com/trulyspinach/SMCAMDProcessor)
 - [[Kext] AppleMCEReporterDisabler v1.0](https://github.com/AMD-OSX/AMD_Vanilla/blob/experimental-opencore/Extra/AppleMCEReporterDisabler.kext.zip)
 - [[Kext] AGPMInjector (Customized for RX580)](https://github.com/Pavo-IM/AGPMInjector)
 - [[Kext] itlwm v1.1.0](https://github.com/OpenIntelWireless/itlwm)
 - [[Kext] IntelBluetoothFirmware v1.1.2](https://github.com/OpenIntelWireless/IntelBluetoothFirmware)
 - [[Kext] IntelBluetoothInjector v1.1.2](https://github.com/OpenIntelWireless/IntelBluetoothFirmware)
 - [[Kext] USBPorts (mobo customized)](https://github.com/headkaze/Hackintool)
 - [[Kext] VoodooTSCSyncAMD-16Cores (CPU customized)](https://www.insanelymac.com/forum/files/file/744-voodootscsync-configurator/)
 - [[Tool] gibMacOS](https://github.com/corpnewt/gibMacOS)
 - [[Tool] GenSMBIOS](https://github.com/corpnewt/GenSMBIOSGenSMBIOS)
 - [[Tool] ProperTree](https://github.com/corpnewt/ProperTreeProperTree)
 <br><br> Many thanks to all the help from AMD-OS X Forums.


# Hackitosh Apps
- Install Homebrew : 
	- /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
- Karabiner :
	- brew cask install karabiner-elements
	- Import settings from karabiner/ folder
	- If doesn't work change keyboard to "virtual" and cahnge to USB Keyboard again
- Hackintool
- OpenCore Configurator


# MacOS Apps
- iTerm2 + Oh My Zsh! :
	- brew cask install iterm2
	- brew install zsh zsh-completions
	- Follow https://www.freecodecamp.org/news/how-to-configure-your-macos-terminal-with-zsh-like-a-pro-c0ab3f3c1156/
- XtraFinder : https://www.trankynam.com/xtrafinder/
- HyperDock : brew install hyperdock
- HyperSwitch : brew install hyperswitch
- CopyQ : brew install copyq
- Caffeine : brew install caffeine
- iStat Menus : brew install istat-menus
- Keka : brew install keka
- Lightshot Screenshot : https://app.prntscr.com/es/download.html
- MonitorControl : brew cask install monitorcontrol
- Numi : brew install numi
- PingMenu : brew cask install pingmenu
- Tunnelblick : brew install tunnelblick
- Sublime Text : brew cask install sublime-text
