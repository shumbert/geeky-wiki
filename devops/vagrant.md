# Vagrant
## Create a Vagrant box (Debian)
### Create VM
- Memory 512MB
- VDI disk 100GB dynamic
- Set pointing device to PS/2 Mouse
- Disable audio
- Disable USB

### OS Installation
- root password is vagrant
- vagrant user (password is vagrant)
- Install SSH server and standard system utilities only

### Configuration (as root)
```
apt install sudo
```

Edit /etc/sudoers.d/vagrant:
```
vagrant ALL=(ALL) NOPASSWD:ALL
```

Edit /etc/ssh/sshd_config and add the following lines:
```
PermitRootLogin no
PasswordAuthentication no
UseDNS no
```

### Install VirtualBox Guest Additions (as root)
```
apt-get install linux-headers-$(uname -r) build-essential dkms
wget http://download.virtualbox.org/virtualbox/5.1.26/VBoxGuestAdditions_5.1.26.iso
mkdir /media/VBoxGuestAdditions
mount -o loop,ro VBoxGuestAdditions_4.3.8.iso /media/VBoxGuestAdditions
sh /media/VBoxGuestAdditions/VBoxLinuxAdditions.run
rm VBoxGuestAdditions_4.3.8.iso
umount /media/VBoxGuestAdditions
rmdir /media/VBoxGuestAdditions
```

### Set the SSH insecure key (as vagrant)
```
mkdir ~/.ssh
wget -O ~/.ssh/authorized_keys https://raw.githubusercontent.com/mitchellh/vagrant/master/keys/vagrant.pub
```

### Clean-up (as root)
```
apt-get clean
cat /dev/null > /home/vagrant/.bash_history
cat /dev/null > /root/.bash_history && history -c && exit
```

### Package the box
```
vagrant package --base stretch64 --output stretch64.box
```

## Create a Vagrant box (OpenBSD)
### Create VM
- Memory 512MB
- VDI disk 15GB dynamic
- Set pointing device to PS/2 Mouse
- Disable audio
- Disable USB

### OS Installation
- root password is vagrant
- vagrant user (password is vagrant)
- everything else is default

### Configuration (as root)
Set up doas:
```
echo 'permit nopass vagrant' > /etc/doas.conf
```

Edit /etc/ssh/sshd_config and add the following lines:
```
PermitRootLogin no
PasswordAuthentication no
UseDNS no
```

### Set the SSH insecure key (as vagrant)
```
ftp https://raw.githubusercontent.com/mitchellh/vagrant/master/keys/vagrant.pub
mv vagrant.pub ~/.ssh/authorized_keys
chmod 0600 ~/.ssh/authorized_keys
```

### Package the box
```
vagrant package --base openbsd --output openbsd66.box
```