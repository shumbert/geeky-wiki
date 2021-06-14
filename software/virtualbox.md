# Install VirtualBox guest additions
## Debian
Do:
```
sudo apt update && sudo apt upgrade
sudo apt install build-essential module-assistant
sudo m-a prepare
```

Then insert Guest Additions CD image and do:
```
sudo mount /media/cdrom
sudo sh /media/cdrom/VBoxLinuxAdditions.run
```

# Manually mount shared folders
If for some reason your Linux distribution does not auto-mount the shared folder, you can manually mount it using the following command:
```
sudo mount -t vboxsf <shared folders> /path/to/mount/point
```

# USB devices do not show up
Go to your machine settings, Devices then USB. If no devices show up make sure your user account in the vboxusers group.

# VERR_PDM_NO_USB_PORTS
By default VirtualBox VMs are created with a USB 1.1 controller. If you plug a USB3 device on a USB3 port on the host you won't be able to attach it to the VM. Update the VM configuration to a USB 3.0 controller.

# Expand disk of LUKS encrypted Linux guest
Instructions from [Expand VirtualBox Debian encrypted disk](https://www.teosoft.it/post/2018-03-19-expand-virtualbox-debian-encrypted-disk/).

## Resize the virtual drive
Increase the size of the virtual drive in virtualbox.

## Update the guest
Boot the virtual machine on [systemrescue](https://www.system-rescue.org/).

Open the encrypted volume:
```
cryptsetup luksOpen /dev/sda5 crypt
```

Extend the partitions:
```
parted /dev/sda
resizepart 2 100%
resizepart 5 100%
quit
```

Deactivate the volume group:
```
vgchange -a n crypt # name from "VG Name" in vgdisplay output
```

Close then re-open the encrypted volume:
```
cryptsetup luksClose crypt
cryptsetup luksOpen /dev/sda5 crypt
```

Resize the LUKS volume:
```
cryptsetup resize crypt-volume
```

Activate the volume group:
```
vgchange -a y crypt
```

Resize the physical volume:
```
pvresize /dev/mapper/crypt
```

Resize the logical volume for /:
```
lvresize -l+100%FREE /dev/crypt/root # path from "LV Path" in lvdisplay output
```

Check the filesystem:
```
e2fsck -f /dev/mapper/crypt-root
```

Resize the filesystem:
```
resize2fs /dev/mapper/crypt-root
```

Finally reboot the virtual machine.

# Shrink a virtual disk
First things first, those instructions only work for a dynamic size VDI virtual disk.

If the VM is not encrypted the process is straight-forward, you just need to zero out empty space then compact the virtual disk:
```
# on the guest
dd if=/dev/zero of=/var/tmp/bigemptyfile bs=4096k ; rm /var/tmp/bigemptyfile

# then shut down the guest and compact the disk from the host
vboxmanage modifymedium --compact __disk_uuid__
```

If the VM is encrypted the process is more convoluted (and quite experimental!):
```
# boot the virtual machine on gparted iso
# open the luks container
sudo cryptsetup luksOpen /dev/sda5 vault

# swap logical volume will be in the way, just delete it
sudo lvremove /dev/crypt/swap_1

# resize the root filesystem
sudo resize2fs /dev/crypt/root/40G

# (you may have to check the filesystem first
sudo e2fsck -f /dev/crypt/root

# resize the logical volume
lvresize -L40G /dev/crypt/root

# resize the physical volume
# (in my case pvresize did not accept 40G, but 41G was ok
pvresize --setphysicalvolumesize 41G /dev/mapper/crypt-volume

# deactivate the volume group then resize the luks container
sudo vgchange -a n crypt
sudo cryptsetup resize vault --device-size 41G
sudo vgchange -a y crypt

# resize the partition in parted:
# (i used 45G here, when i used 40G in resizepart the resulting partition looked significantly smaller than 40G)
sudo parted /dev/sda
parted> resizepart 5 45G

# reboot the virtual machine and with some luck it will boot up!

# finally create an extra partition with parted
sudo parted /dev/sda
parted> unit s print # note down the last sector of the previous partition
parted> mkpart logical ext2 87890626s 100% # as start size use the previous partition last sector + 1

# zero out the new partition
dd if=/dev/zero of=/dev/sda6 bs=4096k

# then shut down the guest and compact the disk from the host
vboxmanage modifymedium --compact __disk_uuid__
```
