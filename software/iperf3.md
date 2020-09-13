# Installation
```
sudo apt install iperf3

# And not iperf!!
```

# Run it (server-side)
```
iperf3 -s -f M
```

# Run it (client-side)
```
# Send data to server
iperf3 -c <server ip> -f M -t 120

# Receive data from server
iperf3 -c <server ip> -f M -R -t 120
```
