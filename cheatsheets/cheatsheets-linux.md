# Linux
## Partition, create filesystem and mount drive
```
parted /dev/disk/by-id/scsi-0DO_Volume_volume-tor1-01 mklabel gpt
parted -a opt /dev/disk/by-id/scsi-0DO_Volume_volume-tor1-01 mkpart primary ext4 0% 100%
mkfs.ext4 /dev/disk/by-id/scsi-0DO_Volume_volume-tor1-01-part1
mkdir -p /mnt/storage/
echo '/dev/disk/by-id/scsi-0DO_Volume_volume-tor1-01-part1 /mnt/storage ext4 defaults,nofail,discard 0 2' | sudo tee -a /etc/fstab
mount -a
```

### List block storage devices
```
lsblk -o NAME,FSTYPE,SIZE,TYPE,MOUNTPOINT
```

## Check whether disks are HDDs are SSDs
```
lsblk -d -o name,rota
```
## Find the most recently updated files in a directory
```
find /path/to/directory/ -printf '%T+ %p\n' | sort -r | head
```

## Display ownership and permissions on a path
```
namei -om /path/to/file
```

## List partition tables
```
gdisk /dev/sdb
GPT fdisk (gdisk) version 1.0.3

Partition table scan:
  MBR: MBR only
  BSD: not present
  APM: not present
  GPT: not present
```