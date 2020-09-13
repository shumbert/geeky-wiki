# Check if disk is SSD or HDD

```
cat /sys/block/sda/queue/rotational
```

You should get 1 for hard disks and 0 for a SSD.

**Note:** it may not work if your disk is a logical device emulated by hardware (like a RAID controller).

# Create a vfat flash drive
First overwrite everything on the flash drive:
```
sudo dd status=progress if=/dev/zero of=/dev/sdb bs=4k && sync
```

Then create a partition:
```
sudo fdisk /dev/sdb
```

Press 'o' to create a new empty DOS partition table, then press 'n' to add a new partition.

Finally format the partition:
```
sudo mkfs.vfat -n 'FLASH' /dev/sdb1
```

#  GRUB and UEFI stuff
- Grub needs the first 2MB at the start of an MBR disk, or a partition of its own on a GPT disk, to install itself. UEFI needs its own partition.
