# Webcam only shows black in skypeforlinux
As described [here](https://askubuntu.com/questions/1005119/skypeforlinux-not-working-with-external-usb-camera):
```
# Install and load v4l2loopback
sudo apt-get install v4l2loopback-dkms
sudo modprobe v4l2loopback

# This will a virtual webcam in /dev/video?

# Then use the following command to redirect the real webcam to the virtual one
ffmpeg -i /dev/video0 -vcodec rawvideo -pix_fmt yuv420p -threads 0 -f v4l2 /dev/video2
```

Configure skype to use the virtual webcam.
