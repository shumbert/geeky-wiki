# Create a bootable FreeDOS USB disk
First download the USB Full installer from http://www.freedos.org/download/. Then extract the image file and copy it to an USB flash drive as such:
```
unzip FD12FULL.zip 
sudo dd if=FD12FULL.img of=/dev/sdX status=progress
```
