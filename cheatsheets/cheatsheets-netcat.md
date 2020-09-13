# netcat
## Scanning
```
# Send QUIT to the server to get some answer from the server (and hopefully some information about the daemon)
echo QUIT | nc -v -w 5 target 20-250 500-600 5990-7000
```
