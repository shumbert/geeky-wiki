# Installation
```
sudo add-apt-repository ppa:wireguard/wireguard && sudo apt-get update && sudo apt-get install openresolv curl linux-headers-$(uname -r) wireguard-dkms wireguard-tools
```

Alternatively you can install the wireguard meta-package from debian sid.

**Note from Mullvad.net guides:** Due to a Debian bug, Debian/Ubuntu users may want to install openresolv rather than Debian's broken resolvconf, in order to prevent DNS leaks.

# Configuration files
Copy configuration files in /etc/wireguard/ then change permission and ownership:
```
sudo chown root:root -R /etc/wireguard/*.conf && sudo chmod 600 -R /etc/wireguard/*.conf
```

# Cheatsheet
## Connect
```
wg-quick up mullvad-se4
```

## Disconnect
```
wg-quick down mullvad-se4
```
