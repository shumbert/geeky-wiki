# Links
- [An overview of Secure Boot in Debian](https://debamax.com/blog/2019/04/19/an-overview-of-secure-boot-in-debian/)
- [Debian releases](https://www.debian.org/releases/)
- [Debian Sources List Generator](https://debgen.simplylinux.ch/)
- [Debian bug tracking system](https://www.debian.org/Bugs/)
- [Debian Package Tracker](https://tracker.debian.org/)

# Debian installer
## Boot parameters
In the first installer screen, press TAB (BIOS boot) or 'e' then down arrow times then end (UEFI boot). Press Enter (BIOS) or F10 (UEFI) to boot the installer with your options.

## Consoles
In text-mode installation use Left Alt + Fn to switch between consoles:
- F1: installer
- F2: shell
- F3: shell
- F4: installer logs

## Partitioning
If you have booted in EFI mode then within the guided partitioning setup there will be an additional partition, formatted as a FAT32 bootable filesystem, for the EFI boot loader. This partition is known as an EFI System Partition (ESP). There is also an additional menu item in the formatting menu to manually set up a partition as an ESP.

# Missing firmware
Unofficial non-free images which include firmware packages:
- https://cdimage.debian.org/cdimage/unofficial/non-free/cd-including-firmware/

# Kernel CPU microcode update on Debian-based systems
On debian-based systems, the kernel can update the CPU microcode. The microcode update is kept in volatile memory, thus the kernel updates the microcode during every boot.

Enable contrib and non-free in /etc/apt/sources.list:
```
deb http://security.debian.org/ stretch/updates main contrib non-free
deb-src http://security.debian.org/ stretch/updates main contrib non-free
deb  http://deb.debian.org/debian stretch main contrib non-free
deb-src  http://deb.debian.org/debian stretch main contrib non-free
```

Then:
```
apt update
apt install amd64-microcode intel-microcode
```

## Check the microcode version
```
dmesg | grep "microcode updated early to"
journalctl -b -k | grep "microcode updated early to"
zgrep "microcode updated early to" /var/log/kern.log*
```

## Disable kernel CPU microcode update
In GRUB2 add the following kernel command line parameter: dis_ucode_ldr.

# ifupdown legacy network configuration
Here is how to switch from network-manager to ifupdown to manage your network interface. Add the following stanza in /etc/network/interfaces:
```
allow-hotplug enp0s3
iface enp0s3 inet static
  address 192.168.11.100/24
  gateway 192.168.11.1
  dns-domain example.com
  dns-nameservers 192.168.11.1
```

Then install the resolvconf package (required for automatically managing /etc/resolv.conf). Finally reboot.

To update your interface settings, update /etc/network/interfaces then do:
```
sudo ifdown enp0s3 && sudo ifup enp0s3
```

**Note:** the allow-hotplug stanza causes ifup to bring up the interface and the iface stanza causes ifup to configure the interface.

**Note:** the systemd unit networking.service is only meant for the loopback interface. Don't restart it to apply changes it will just leave your network interface unconfigured.

**Note:** network-manager will only manage interfaces which are not defined in /etc/network/interfaces.

Some typical ip commands:
```
# Show interface
ip addr
ip addr show

# Show routes
ip route
ip route show

# Show arp neighbours
ip neigh
ip neigh show
```

# Nftables
There is a [wiki](https://wiki.nftables.org/wiki-nftables/index.php/Main_Page).

# Emojis
Get those emoji fonts:
```
sudo apt install fonts-noto-color-emoji
```

# DPKG-fu
```
# List files in package
dpkg -L base-passwd

# Search file in installed packages
dpkg -S /bin/date

# Show status of package
dpkg -s coreutils

# List packages matching b*
dpkg -l 'b*'

# List contents of deb package
dpkg -c /var/cache/apt/archives/gnupg_1.4.18-6_amd64.deb

# Show info on deb package
dpkg -I /var/cache/apt/archives/gnupg_1.4.18-6_amd64.deb
```

# APT-fu
## Hold packages
```
sudo apt-mark hold <package>
sudo apt-mark unhold <package>
apt-mark showhold
```

## Versions
```
apt-cache policy <package>
apt-cache madison <package>
```

## Misc APT commands
```
# Lists available package versions with distribution
apt-show-versions

# Show new changelog entries from Debian package archives
apt-listchanges
```

# Packaging
## Links
- [Debian Policy Manual](https://www.debian.org/doc/debian-policy/index.html)
- [Pragmatic Debian Packaging](https://vincent.bernat.ch/en/blog/2019-pragmatic-debian-packaging)
- [How To Package For Debian](https://wiki.debian.org/HowToPackageForDebian)
- [Intro to Debian Packaging](https://wiki.debian.org/Packaging/Intro?action=show&redirect=IntroDebianPackaging)
- [Packages maintained by the Debian Go Packaging Team](https://salsa.debian.org/go-team/packages)

## Some useful commands
```
# create package
dpkg-buildpackage -us -uc -b

# check package content
dpkg -c <package>

# check info (and dependencies)
dpkg -I ../gitlab-audit_0.0-0_amd64.deb | grep Depends
```