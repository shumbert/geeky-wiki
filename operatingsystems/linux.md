# Linux links
- [Linux Performance](http://www.brendangregg.com/linuxperf.html)
- [Kernel analysis with bpftrace](https://lwn.net/Articles/793749/)
- [Use oathtool Linux command line for 2 step verification (2FA)](https://www.cyberciti.biz/faq/use-oathtool-linux-command-line-for-2-step-verification-2fa/)
- [What has to happen with Unix virtual memory when you have no swap space](https://utcc.utoronto.ca/~cks/space/blog/unix/NoSwapConsequence)
- [How fast are your disks? Find out the open source way, with fio](https://arstechnica.com/gadgets/2020/02/how-fast-are-your-disks-find-out-the-open-source-way-with-fio/)
- [Intercepting Zoom's encrypted data with BPF](https://confused.ai/posts/intercepting-zoom-tls-encryption-bpf-uprobes)

# Lock a user account
```
# Expire an account
# if the account is expired user won't be able to login via password nor ssh public key
sudo chage -E 0 <username>

# Check expiration status
sudo chage -l <username>

# Un-expire an account
sudo chage -E -1 <username>
```

# Partition, create filesystem and mount drive
```
parted /dev/disk/by-id/scsi-0DO_Volume_volume-tor1-01 mklabel gpt
parted -a opt /dev/disk/by-id/scsi-0DO_Volume_volume-tor1-01 mkpart primary ext4 0% 100%
mkfs.ext4 /dev/disk/by-id/scsi-0DO_Volume_volume-tor1-01-part1
mkdir -p /mnt/storage/
echo '/dev/disk/by-id/scsi-0DO_Volume_volume-tor1-01-part1 /mnt/storage ext4 defaults,nofail,discard 0 2' | sudo tee -a /etc/fstab
mount -a
```

# List partition tables
```
gdisk /dev/sdb
GPT fdisk (gdisk) version 1.0.3

Partition table scan:
  MBR: MBR only
  BSD: not present
  APM: not present
  GPT: not present
```

# Check if disk is SSD or HDD

```
cat /sys/block/sda/queue/rotational
```

You should get 1 for hard disks and 0 for a SSD.

**Note:** it may not work if your disk is a logical device emulated by hardware (like a RAID controller).

You can also use:
```
lsblk -d -o name,rota
```

# Find the most recently updated files in a directory
```
find /path/to/directory/ -printf '%T+ %p\n' | sort -r | head
```

# Display ownership and permissions on a path
```
namei -om /path/to/file
```

# List partition tables
```
gdisk /dev/sdb
GPT fdisk (gdisk) version 1.0.3

Partition table scan:
  MBR: MBR only
  BSD: not present
  APM: not present
  GPT: not present
```

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

Alternatively format the partition as exFAT to go past the FAT32 file size limit (4GB):
```
# recent Linux distributions should have built-in support for exFAT
# but if mkfs.exfat does not exist on your system install those packages
sudo apt install exfat-fuse exfat-utils

sudo mkfs.exfat -n 'FLASH' /dev/sdb1
```

#  GRUB and UEFI stuff
- Grub needs the first 2MB at the start of an MBR disk, or a partition of its own on a GPT disk, to install itself. UEFI needs its own partition.
