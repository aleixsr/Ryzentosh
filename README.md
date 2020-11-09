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
 	Settings → IO Ports → USB Configuration → XHCI Hand-off : Enabled
 	Boot → Fast Boot : Disabled
 	Boot → CMS Support : Disabled
 	Boot → Secure Boot → Secure Boot : Disabled
 	+BIOS ADVANCED SETTINGS


## Post Installation
- LAN Network: Not Connected
1.- System Preferences → Network  → Select your Ethernet controller. Normally it says (not connected).  → Advanced → Hardware:
	- Switch from Automatically to Manually
	- Speed : 1000baseT (if doesn't work 100baseTX
	- Duplex : full-duplex, flow-control, energy-efficient-ethernet
	- MTU : Standard (1500)

- Move your OpenCore EFI folder to a MacOS drive: https://dortania.github.io/OpenCore-Post-Install/universal/oc2hdd.html#grabbing-opencore-off-the-usb

# Hackitosh Apps
- Install Homebrew : /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"

- Karabiner : brew cask install karabiner-elements
	Import settings from karabiner/ folder
	If doesn't work change keyboard to "virtual" and Keyb again

- Hackintool

- OpenCore Configurator

# MacOS Apps
- iTerm2 + Oh My Zsh! : brew cask install iterm2
	brew install zsh zsh-completions
	sudo sh -c "echo $(which zsh) >> /etc/shells"
	chsh -s $(which zsh)
	sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
	git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/.powerlevel10k
	echo "source ~/.powerlevel10k/powerlevel10k.zsh-theme" >>! ~/.zshrc	
	git clone https://github.com/powerline/fonts.git --depth=1
	cd fonts
	./install.sh
	cd ..
	rm -rf fonts
	Open iTerm Acceder a “iTerm > Preferences > Profiles > Text”
	Seleccionar la fuente "Meslo LG S Powerline" o alguna fuente de las entregadas por powerline.
	cd ~/.oh-my-zsh/custom/plugins
	git clone https://github.com/zsh-users/zsh-syntax-highlighting
	git clone https://github.com/zsh-users/zsh-autosuggestions
	vim ~/.zshrc
	ZSH_THEME="agnoster"
	pligons
	plugins=(
        git
        zsh-autosuggestions
        zsh-syntax-highlighting
)
	Colors Batman
- XtraFinder
- HyperDock
- HyperSwitch
- 1Clipboard : brew cask install 1clipboard (or CopyQ)
- Caffeine
- iStat Menus
- Keka
- Lightshot Screenshot
- MonitorControl : brew cask install monitrocontrol
- Numi
- PingMenu
- Rectangle?
- Tunnelblick

