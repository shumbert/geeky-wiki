# journald
journald collects logs from various sources (including systemd services) and store them:
- in a in-memory buffer (/run/log/journal) if persistence is disabled (or during early stages of boot)
- on disk (/var/log/journal) if persistence is enabled

To enable persistence, edit /etc/systemd/journald.conf:
```
Storage=persistent
```

Then restart journald:
```
systemctl restart systemd-journald
```

To check size of both runtime (in-memory buffer) and system (on disk) journals:
```
journalctl -u systemd-journald
```

By default max size of both runtime and system journals is 10% of the underlying file system. More elaborate description:

<em>SystemMaxUse= and RuntimeMaxUse= control how much disk space the journal may use up at most.  SystemKeepFree= and RuntimeKeepFree= control how much disk space systemd-journald shall leave free for other uses. systemd-journald will respect both limits and use the smaller of the two values.</em>

<em>The first pair defaults to 10% and the second to 15% of the size of the respective file system, but each value is capped to 4G. If the file system is nearly full and either SystemKeepFree= or RuntimeKeepFree= are violated when systemd-journald is started, the limit will be raised to the percentage that is actually free. This means that if there was enough free space before and journal files were created, and subsequently something else causes the file system to fill up, journald will stop using more space, but it will not be removing existing files to reduce the footprint again, either. Also note that only archived files are deleted to reduce the space occupied by journal files. This means that, in effect, there might still be more space used than SystemMaxUse= or RuntimeMaxUse= limit after a vacuuming operation is complete.</em>

# Resolved
systemd-resolved is a DNS caching resolver. Check out the [Arch Wiki](https://wiki.archlinux.org/index.php/Systemd-resolved) entry.

In distributions using systemd-resolved such as Ubuntu /etc/resolv.conf is managed by systemd-resolved:
```
nameserver 127.0.0.53
```

systemd-resolved can be queried/managed via resolvectl:
```
# check status
resolvectl status

# flush local cache
resolvectl flush-caches

# currently no command to dump entries from the local cache
```
