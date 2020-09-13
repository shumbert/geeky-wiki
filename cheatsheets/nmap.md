# Nmap
## TCP SYN Scan (needs root)
```
nmap -sS <target>
```

## Specify port range (1-1024 only by default)
```
nmap -sS -p <lower>-<upper> <target>
```

## Scan all ports
```
nmap -sS -p- <target>
```

## Version detection scan
```
nmap -sV -p port1,port2,... <target>
```
