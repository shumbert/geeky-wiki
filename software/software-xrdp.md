# Setup (xfce4)
The following is for setting up a VPS with xrdp and xfce4. First install packages:
```
sudo tasksel install xfce-desktop
sudo apt install xrdp xorgxrdp
sudo systemctl stop lightdm
sudo systemctl disable lightdm
```

Edit /etc/xrdp/startwm.sh:
```
#test -x /etc/X11/Xsession && exec /etc/X11/Xsession
#exec /bin/sh /etc/X11/Xsession
startxfce4
```

Edit /etc/X11/Xwrapper.conf:
```
allowed_users=anybody
```

And finally reboot.

**Note:** Xwrapper.config may be overwritten when updating Xorg packages. If configuration is back to default(allowed_users=console), you just see a blank screen after logging in and eventually an error message. Restore the config to fix this.

# Setup (Ubuntu 18.04 LTS)
Instructions from [here](https://www.hiroom2.com/2018/04/29/ubuntu-1804-xrdp-gnome-en/). Polkit configuration from [here](https://c-nergy.be/blog/?p=12073).

## Install packages
```
sudo apt install -y xrdp xorgxrdp-hwe-18.04
```

## Configure xrdp
```
sudo sed -e 's/^new_cursors=true/new_cursors=false/g' -i /etc/xrdp/xrdp.ini
sudo systemctl restart xrdp
```

## Configure polkit
```
cat <<EOF | sudo tee /etc/polkit-1/localauthority.conf.d/02-allow-colord.conf
polkit.addRule(function(action, subject) {
 if ((action.id == "org.freedesktop.color-manager.create-device" ||
 action.id == "org.freedesktop.color-manager.create-profile" ||
 action.id == "org.freedesktop.color-manager.delete-device" ||
 action.id == "org.freedesktop.color-manager.delete-profile" ||
 action.id == "org.freedesktop.color-manager.modify-device" ||
 action.id == "org.freedesktop.color-manager.modify-profile") &&
 subject.isInGroup("{users}")) {
 return polkit.Result.YES;
 }
 });
EOF
sudo systemctl restart polkit
```

## Create .xsessionrc
```
D=/usr/share/ubuntu:/usr/local/share:/usr/share:/var/lib/snapd/desktop
cat <<EOF > ~/.xsessionrc
export GNOME_SHELL_SESSION_MODE=ubuntu
export XDG_CURRENT_DESKTOP=ubuntu:GNOME
export XDG_DATA_DIRS=${D}
export XDG_CONFIG_DIRS=/etc/xdg/xdg-ubuntu:/etc/xdg
EOF
```

# Thin client drives
xrdp mounts a drive for Chansrv (using for clipboard redirection among other things). Default path is $HOME/thinclient_drives, you can hide the folder by changing a setting in /etc/rxdp/sesman.ini:
```
[Chansrv]
FuseMountName=.thinclient_drives
```

# Remmina
To connect to xrdp from remmina, make sure the following option is enabled in the advanced settings:
- Glyph Cache