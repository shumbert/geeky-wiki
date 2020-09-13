# Ubuntu links
- [multipass](https://multipass.run/)

# Install Chinese fonts
Tested on Ubuntu 14.04:
```
sudo apt-get install fonts-wqy-zenhei
```

# Secure boot and 3rd party modules
When you install a 3rd party module on a secure-boot enabled ubuntu machine:
- to permit use of third-party drivers, a new machine-owner key has been generated (MOK) and needs to be enrolled in the system firmware
- you must choose a password now and confirm that same password at next boot in both the "Enroll MOK" and "CHange Secure boot state"
- if password is not confirmed, ubuntu will boot but any third-party modules won't be loaded

# ZFS on root
## Some links
- [Arc Technica - A detailed look at Ubuntu’s new experimental ZFS installer](https://arstechnica.com/information-technology/2019/10/a-detailed-look-at-ubuntus-new-experimental-zfs-installer/)
- [Ubuntu ZFS support in 19.10: ZFS on root](https://didrocks.fr/2019/10/11/ubuntu-zfs-support-in-19.10-zfs-on-root/)
- [New ubuntu 20.04 install, zfs on root — root and boot filling up](https://askubuntu.com/questions/1242935/new-ubuntu-20-04-install-zfs-on-root-root-and-boot-filling-up)
- [OpenZFS documentation](https://openzfs.github.io/openzfs-docs/)

## Some Notes
- ZFS is included in modern Linux kernel, it's technically possible to set up ZFS on root for all major distros (check the OpenZFS documentation).
- Ubuntu goes a bit further by including ZFS on root support in their installer, you just need to check the option in the disk partitioning stage.
- However snapshot management is not fully integrated. There is a tool (zsys) for taking snapshots, for instance whenever you install/update packages new snapshots are automatically taken. But there is no graphical tool for snapshot management. To restore snapshots you have to use the zfs command-line tool.
- Also by default the installer creates a lot of datasets (see below), that seems overkill especially considering that most systems are now setup with a single partition. That part feels a bit over-engineered.

## Default Ubuntu ZFS on root setup.
One ZFS partition for the “rpool” (as root pool), which will contain your main installation and user data. Another ZFS partition for your boot pool named “bpool”, which contains kernels and initramfs (basically your /boot without the EFI and bootloader).

Note that due to this, even if zpool status proposes that you to upgrade your bpool, you should never do that or you won’t be able to reboot.

List of datasets:
```
simal@focal:~$ zfs list
NAME                                               USED  AVAIL     REFER  MOUNTPOINT
bpool                                              180M   651M       96K  /boot
bpool/BOOT                                         180M   651M       96K  none
bpool/BOOT/ubuntu_tam513                           180M   651M      180M  /boot
rpool                                             3.57G  13.4G       96K  /
rpool/ROOT                                        3.52G  13.4G       96K  none
rpool/ROOT/ubuntu_tam513                          3.52G  13.4G     2.94G  /
rpool/ROOT/ubuntu_tam513/srv                        96K  13.4G       96K  /srv
rpool/ROOT/ubuntu_tam513/usr                       224K  13.4G       96K  /usr
rpool/ROOT/ubuntu_tam513/usr/local                 128K  13.4G      128K  /usr/local
rpool/ROOT/ubuntu_tam513/var                       536M  13.4G       96K  /var
rpool/ROOT/ubuntu_tam513/var/games                  96K  13.4G       96K  /var/games
rpool/ROOT/ubuntu_tam513/var/lib                   531M  13.4G      436M  /var/lib
rpool/ROOT/ubuntu_tam513/var/lib/AccountsService   160K  13.4G       96K  /var/lib/AccountsService
rpool/ROOT/ubuntu_tam513/var/lib/NetworkManager    212K  13.4G      124K  /var/lib/NetworkManager
rpool/ROOT/ubuntu_tam513/var/lib/apt              58.2M  13.4G     58.1M  /var/lib/apt
rpool/ROOT/ubuntu_tam513/var/lib/dpkg             36.0M  13.4G     33.4M  /var/lib/dpkg
rpool/ROOT/ubuntu_tam513/var/log                  4.36M  13.4G     3.05M  /var/log
rpool/ROOT/ubuntu_tam513/var/mail                   96K  13.4G       96K  /var/mail
rpool/ROOT/ubuntu_tam513/var/snap                  104K  13.4G      104K  /var/snap
rpool/ROOT/ubuntu_tam513/var/spool                 168K  13.4G      112K  /var/spool
rpool/ROOT/ubuntu_tam513/var/www                    96K  13.4G       96K  /var/www
rpool/USERDATA                                    46.4M  13.4G       96K  /
rpool/USERDATA/root_ccmc0i                         176K  13.4G      112K  /root
rpool/USERDATA/simal_ccmc0i                       46.2M  13.4G     38.1M  /home/simal
```

List of pools:
```
simal@focal:~$ zpool list -v -H -P
bpool	960M	181M	779M	-	-	1%	18%	1.00x	ONLINE	-
	/dev/sda6	960M	181M	779M	-	-	1%	18.8%	-	ONLINE  
rpool	17.5G	3.57G	13.9G	-	-	4%	20%	1.00x	ONLINE	-
	/dev/sda7	17.5G	3.57G	13.9G	-	-	4%	20.4%	-	ONLINE
```

There is the ESP partition (mounted as /boot/efi). Right now, it’s only created if you have a UEFI system, but we might get it created in Ubiquity systematically in the future, so that people who disabled secure boot and enable it later on can have a smooth transition.

Test snapshot restore:
```
# take a snapshot
zfs snapshot -r rpool@before-apt

# check snapshots
zfs list -rt snap rpool | grep before-apt | awk '{print $1}' | head

# now do something like removing firefox

# restore the previous snapshot
zfs list -rt snap rpool | grep before-apt | awk '{print $1}' | xargs -I% sudo zfs rollback -r %

# now firefox is back!
```
