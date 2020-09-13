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