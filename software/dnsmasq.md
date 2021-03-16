# Set up dnsmasq as a quick and dirty dns server
i want to:
- intercept some A and PTR queries and return some custom results
- pass everything else to upstream servers

On debian install dnsmasq:
```
sudo apt install dnsmasq
```

Edit dnsmasq default config:
```
# we do not want dnsmasq to read /etc/resolv.conf to get upstream servers
no-resolv

# we define them manually instead
server=8.8.8.8

# define some custom A records
address=/my.test.domain/1.2.3.4

# then do the same for PTR records
ptr-record=4.3.2.1.in-addr.arpa,my.test.domain

# in default debian config, dnsmasq binds 0.0.0.0 however it only listens for queries coming on lo
# you have to explicitely set which interfaces dnsmasq will accept queries from
interface=lo
interface=enp0s3
```

Test everything is peachy using dig:
```
sudo apt install dnsutils
dig my.test.domain @localhost
dig -x 1.2.3.4 @localhost
```

Finally override the DNS server obtained from DHCP by editing /etc/dhcp/dhclient.conf:
```
supersede domain-name-servers 127.0.01;
```

Then reboot!
