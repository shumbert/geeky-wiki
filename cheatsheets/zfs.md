# ZFS
## Miscellaneous commands
```
zpool status
```

## Replace a faulty drive
Issue the following command:
```
zpool offline vtbd3
```

Then replace and partition the drive. Then issue the following command:
```
zpool replace storage vtbd3
```

## Replace an unavailable drive
Replace and partition the drive. Then issue the following commands:
```
zpool status storage (check the GUID of the missing drive)
zpool replace storage 264926568307219235 vtbd3
```
