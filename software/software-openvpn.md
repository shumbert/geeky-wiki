# Run openvpn so that it update the DNS settings
```
sudo apt install openresolv
sudo openvpn --config config.ovpn --up /etc/openvpn/update-resolv-conf --down /etc/openvpn/update-resolv-conf --script-security 2
```
