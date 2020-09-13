# Linux Software RAID
## Some links
- [ArchWiki: RAID](https://wiki.archlinux.org/index.php/RAID)
- [Linux RAID](https://raid.wiki.kernel.org/index.php/Linux_Raid)

## RAID and root filesystem
For a standard RAID1 setup with 2 drives it is tempting to replicate with software RAID what you would do with hardware RAID, i.e. have the full operating system on the RAID1 array, and the hardware booting with both or either drives.

But there are two issues I can see:
- chicken and egg: the array is managed by the operating system, which is itself on the array. Not sure how big of a problem it is, but it might cause some maintenance headaches.
- MBR and EFI partitions are not properly handled:
  - for BIOS booting, it is relatively straight-forward. You have to manually run grub-install on both disks. (but what if GRUB code is updated in the future?)
  - for UEFI booting, it is way more complicated, as explained [here](https://outflux.net/blog/archives/2018/04/19/uefi-booting-and-raid1/)

To keep things manageable it seems like a better option to use standard partitioning for the root filesystem, and only use RAID1 for the important data.

## Partitioning
Make sure that the system can be booted with the partitioning scheme you are planning. In general it will be necessary to create a separate file system for /boot when using RAID for the root (/) file system. Most boot loaders (including lilo and grub) do support mirrored (not striped!) RAID1, so using for example RAID5 for / and RAID1 for /boot can be an option. Bootloaders reading the boot partition do not understand RAID, but a RAID 1 component partition can be read as a normal partition

If the EFI System Partition is to be located on a RAID array:
- ESP can only be placed on a RAID1 array
- RAID superblock must be placed at the end of the partition. Use ```--metadata=1.0``` when creating the array.

For instance:
```
mdadm --create --verbose --level=1 --metadata=1.0 --raid-devices=2 /dev/md/ESP /dev/sda2 /dev/sdb2
```

## MDADM configuration file
/etc/mdadm/mdadm.conf lists RAID arrays to be started at boot. Whenever you create or delete an array, you should updated /etc/mdadm/mdadm.conf accordingly. You can use the following command:
```
mdadm --detail --scan >> /etc/mdadm/mdadm.conf
```

After updating mdadm.conf, update the initramfs:
```
update-initramfs -u
```

## Create an array
First if the device is being re-purposed from an existing array, erase any old RAID configuration information:
```
sudo mdadm --misc --zero-superblock /dev/sda
```

You can use whole disks for RAID arrays, but it's preferrable to use partitions. Create a partition with fdisk and use type 29 (Linux RAID).

Create the array:
```
sudo mdadm --create --verbose --level=1 --metadata=1.2 --raid-devices=2 /dev/md/storage /dev/sda1 /dev/sdb1
```

The array is created under the virtual device /dev/mdX, assembled and ready to use (in degraded mode). One can directly start using it while mdadm resyncs the array in the background. It can take a long time to restore parity. Check the progress with ```cat /proc/mdstat```.

## Start or stop an array
To start an array:
```
sudo mdadm --assemble --scan # to start all arrays defined in mdadm.conf
sudo mdadm --assemble /dev/md0
```

To stop an array:
```
sudo umount /mnt/md0
sudo mdadm --stop --scan # to stop all arrays defined in mdadm.conf
sudo mdadm --stop /dev/md0
```

## Check arrays
Use the following commands:
```
sudo cat /proc/mdstat
sudo mdadm -D /dev/md0
```

To monitor an array use:
```
sudo mdadm --monitor --scan --mail alice@example.com
```

## Remove or replace a drive
If you need to remove a drive that does not have a problem, you can manually mark it as failed with the --fail option:
```
sudo mdadm /dev/md0 --fail /dev/sdc1
```

Once the device is failed, you can remove it from the array with mdadm --remove:
```
sudo mdadm /dev/md0 --remove /dev/sdc1
```

You can then replace it with a new drive:
```
sudo mdadm /dev/md0 --add /dev/sdd1
```

## Delete an array
First, unmount the filesystem:
```
sudo umount /mnt/md0
```

Next stop the array:
```
sudo mdadm --stop /dev/md0
```

Afterwards, delete the array itself with the --remove command targeting the RAID device (on some distros this might be unnecessary as the stop command will also remove the array):
```
sudo mdadm --remove /dev/md0
```

Finally remove RAID superblocks from the RAID devices:
```
# For whole disks
sudo mdadm --zero-superblock /dev/sda /dev/sdb

# For partitions
sudo mdadm --zero-superblock /dev/sda1 /dev/sdb1
```

## Scrubbing
To scrub a RAID array:
```
echo check > /sys/block/md0/md/sync_action
```

Check status of scrub operation by reading /proc/mdstat.

The check operation scans the drives for bad sectors and automatically repairs them. If it finds good sectors that contain bad data (the data in a sector does not agree with what the data from another disk indicates that it should be, for example the parity block + the other data blocks would cause us to think that this data block is incorrect), then no action is taken, but the event is logged (see below).

To stop a currently running data scrub safely:
```
echo idle > /sys/block/md0/md/sync_action
```

## Debian installer (BIOS boot): set up software RAID + full disk encryption + LVM
- Partitioning method: Manual
  - Select both hard drives and create new empty partition tables

- On both drives create two partitions:
  - 512MB, primary, use as physical volume for RAID, bootable flag on
  - use remaining space, primary, use as physical volume for RAID

- Configure software RAID and create MD devices:
  - RAID1, two primary devices, no spare devices, use /dev/sda1 and /dev/sdb1
  - RAID1, two primary devices, no spare devices, use /dev/sda2 and /dev/sdb2

- Configure encrypted volumes:
  - create encrypted volume on /dev/md1

- Configure logical volume manager:
  - create volume group (use hostname)
  - select /dev/mapper/md1_crypt as physical volume
  - create logical volumes:
    - root (all available space except the one reserved for swap)
    - swap (all remaining space)

- Create /boot partition on /dev/md0:
  - ext2 filesystem
  - mount point /boot

- Create / partition on root logical volume:
  - use as ext4
  - mount point /

- Create swap partition on swap logical volume:
  - use as swap partition

After installation, install grub on second drive:
```
grub-install /dev/sdb
```

## Misc commands:
```
mdadm /dev/mdN --re-add /dev/sdX1
mdadm --assemble /dev/md0 /dev/sda1 /dev/sdb1

# Check array status
mdadm --detail /dev/md0

# if a drive is failed, replace it, create partitions (use Linux Raid partition type, hex code fd)
# then use the following commands:
mdadm --add /dev/md0 /dev/sda1
mdadm --add /dev/md1 /dev/sda2

# Arrays should rebuild automatically.

# Finally re-install grub on the new disk:
grub-install /dev/sda
```
