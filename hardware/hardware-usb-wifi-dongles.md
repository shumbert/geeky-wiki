# TP-Link TL-WN823N
## Make it work on Debian Buster
TP-Link TL-WN823N uses chipset RTL8192EU. First step get firmware:
1. Edit /etc/apt/sources.list and add non-free packages
2. ```sudo apt update```
3. ```sudo apt install firmware-realtek```

Then the system should bring up the network adapter using the rtl8xxxu default driver. But there are 2 major issues:
- signal is very weak
- authentication timeouts when attempting to join a network

Use the rtl8192eu driver instead by following instructions [here](https://github.com/clnhub/rtl8192eu-linux). Things get better however password is not accepted when attempting to join a network. Create file /etc/NetworkManager/conf.d/30-mac-randomization.conf with the following contents:
```
# disable MAC randomization during Wifi scan
# as this leads to (some) USB WLAN adapters not
# being able to connect to a WLAN network,
# s. Debian bug #839605.
[device-mac-randomization]
wifi.scan-rand-mac-address=no
```
