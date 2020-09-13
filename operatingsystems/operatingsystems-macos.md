# Running macoS
## Some shortcuts
| Shortcut | Keys | Comment |
|---|---|---|
| Mission control | CTRL+up | Used to be called expose, you can create new spaces from there |
| Exit mission control | CTRL-down | |
| Switch to space on the left | CTRL-left | |
| Switch to space on the right | CTRL-right | |
| Show spotlight search | Win+space | |
| Move focus to next window | Ctrl+F4 | |
| Minimize front window to the Dock | Command-M | |
| Command-Tab | App switcher | |
| Command-W | Close window | |
| Command-H | Hide app | |
| Command-Q | Quit app | |

## Finder shortcuts
| Shortcut | Keys | Comment |
|---|---|---|
| Command-I | Show the Get Info window for a selected file | |
| Shift-Command-H | Open the Home folder of the current macOS user account | |
| Option-Command-L | Open the Downloads folder | |
| Shift+Command+A | applications | |
| Shift+Command+U | utilities | |

## GUI tricks
- Option and click on + button: maximize window
- Option key while dragging: Copy the dragged item. The pointer changes while you drag the item
- Option-Command while dragging: Make an alias of the dragged item. The pointer changes while you drag the item
- Option–Left Arrow: Move the insertion point to the beginning of the previous word
- Option–Right Arrow: Move the insertion point to the end of the next word
- On your Mac in a Finder window or on the desktop, select one or more items, then press the Space bar. A Quick Look window opens. If you selected multiple items, the first item is shown.

## Brew
### Terminology
| Term | Description | Example |
|---|---|---|
| Formula | The package definition |/usr/local/Homebrew/Library/Taps/homebrew/homebrew-core/Formula/foo.rb |
| Keg | The installation prefix of a Formula | /usr/local/Cellar/foo/0.1 |
| Cellar | All Kegs are installed here | /usr/local/Cellar |
| Tap | A Git repository of Formulae and/or commands | /usr/local/Homebrew/Library/Taps/homebrew/homebrew-core |
| Bottle | Pre-built Keg used instead of building from source | qt-4.8.4.mavericks.bottle.tar.gz |
| Cask | An extension of Homebrew to install macOS native apps | /Applications/MacDown.app/Contents/SharedSupport /bin/macdown |

### Notes
- Homebrew installs packages to their own directory and then symlinks their files into /usr/local.
- Homebrew refuses to work using sudo (or so say the docukmentation).
- All the default formulae from [homebrew-core](https://github.com/Homebrew/homebrew-core) are bottled.

### Useful commands
```
# update the formulae and Homebrew itself
brew update

# find outdated formulae
brew outdated

# upgrade everything
brew upgrade

# list installed formulae
brew list

# list installed casks
brew cask list
```

# Create a bootable macOS ISO
Download macOS High Sierra:
- open App Store, search for High Sierra and click Download
- the installer will launch, just close it with Command+Q

In a terminal enter the following commands:
```
hdiutil create -o /tmp/HighSierra.cdr -size 7316m -layout SPUD -fs HFS+J
hdiutil attach /tmp/HighSierra.cdr.dmg -noverify -nobrowse -mountpoint /Volumes/install_build
asr restore -source /Applications/Install\ macOS\ High\ Sierra.app/Contents/SharedSupport/BaseSystem.dmg -target /Volumes/install_build -noprompt -noverify -erase
hdiutil detach /Volumes/OS\ X\ Base\ System
hdiutil convert /tmp/HighSierra.cdr.dmg -format UDTO -o /tmp/HighSierra.iso
mv /tmp/HighSierra.iso.cdr ~/Desktop/HighSierra.iso
```

# Run macOS High Sierra in VirtualBox
**Note:** based on https://www.howtogeek.com/289594/how-to-install-macos-sierra-in-virtualbox-on-windows-10/

## Create the VM
Create the VM using the following settings:
- OS: Mac OS X
- Version: Mac OS X (64-bit)
- memory: >4096MB

Then open the VM settings:
- System > Motherboard: remove floppy from boot order
- System > Processor: use 2 vCPUs at least
- Display > Screen: use 128MB at least
- connect the macOS ISO to the virtual CD-ROM drive

Finally in a shell use the following commands:
```
VBoxManage setextradata "HighSierra" "VBoxInternal/Devices/efi/0/Config/DmiSystemProduct" "MacBookPro11,3"
VBoxManage setextradata "HighSierra" "VBoxInternal/Devices/efi/0/Config/DmiSystemVersion" "1.0"
VBoxManage setextradata "HighSierra" "VBoxInternal/Devices/efi/0/Config/DmiBoardProduct" "Mac-2BD1B31983FE1663"
VBoxManage setextradata "HighSierra" "VBoxInternal/Devices/smc/0/Config/DeviceKey" "ourhardworkbythesewordsguardedpleasedontsteal(c)AppleComputerInc"
VBoxManage setextradata "HighSierra" "VBoxInternal/Devices/smc/0/Config/GetKeyFromRealSMC" 1
```

## Install macOS
Start the VM, launch the Disk Utility (you may have to select "Show All Devices" in the View menu). Select the VBOX hard drive and click Erase:
- Name: Macintosh HD
- Format: Mac OS Extended (Journaled)
- Scheme: GUID Partition Map

Click on "reinstall macOS" to start the installation. At some point the virtual machine will restart and boot once more on the installation ISO. Just shut down the VM, remove the ISO then start it again.

At this point you will see the EFI internal shell, enter the following command:
```
fs1:
cd "macOS Install Data"
cd "Locked Files"
cd "Boot Files"
boot.efi
```

Then finish the installation.

## Change the resolution
Shut down VM, exit VirtualBox then enter the following command:
```
VBoxManage setextradata "HighSierra" VBoxInternal2/EfiGraphicsResolution 1440x900
```

## Shared folders
No Virtualbox additions for macOS, to share a folder you have to do it the other way around.

### Enable File sharing in the guest
- Go to System Preferences > Sharing
- Enable File Sharing
- Go to Options
- Under Windows File Sharing check the box for your user account
- **your password will be stored in less secure manner**: not sure how secure it is for permanent setups

### Set up port forwarding to the guest
- this following assumes you have a NAT network adapter on your VM
- in Virtualbox VM settings, go to Network
- in the network adapter tab expand Advanced and click on Port forwarding
- add a TCP port forwarding from 127.0.0.1:<host_port> to port 445

### Connect to the shared folder from the host
- in your file manager connect to smb://127.0.0.1:<host_port>
- open the guest os user Public folder
