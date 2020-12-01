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

# Resize disk of LUKS encrypted Linux guest
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
