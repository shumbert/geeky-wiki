# Install tools (on debian/ubuntu)
```
sudo apt install qrencode zbar-tools
```

# Decode a QR code
```
zbarimg image.png
```

# Encode a QR code
```
qrencode -t ansiutf8 < file
qrencode -t ansiutf8 "https://google.com"
```
