To restore a backed-up directory as it was at a given date and time:
```
SpiderOakONE --verbose --restore /path/to/directory/ --point-in-time 2020-01-01/11:30 --output /tmp
```

Some useful commands:
```
# List user devices
SpiderOakONE --userinfo

# Show the spideroak changelog
SpiderOakONE --verbose --tree-changelog > /tmp/changelog
SpiderOakONE --verbose --tree-changelog --device 1 > /tmp/changelog

# Restore backups from a different device
SpiderOakONE --verbose --restore /path/to/directory/ --point-in-time 2020-01-01/11:30 --output /tmp --device 1
```
