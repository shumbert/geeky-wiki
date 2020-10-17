# Setup
## Debian
```
wget https://pkg.tarsnap.com/tarsnap-deb-packaging-key.asc
sudo apt-key add tarsnap-deb-packaging-key.asc
echo "deb http://pkg.tarsnap.com/deb/$(lsb_release -s -c) ./" | sudo tee -a /etc/apt/sources.list.d/tarsnap.list
sudo apt-get update
sudo apt install tarsnap
```

## OpenBSD
Tarsnap first:
```
ftp https://www.tarsnap.com/download/tarsnap-autoconf-1.0.39.tgz
tar xzf tarsnap-autoconf-1.0.39.tgz
cd tarsnap-autoconf-1.0.39
./configure
make all
doas make install
```

Then tarsnapper:
```
pkg_add py-pip
pip2.7 install tarsnapper
```

## Create a key
```
tarsnap-keygen --keyfile <keyfile> --user <username> --machine <machine>
```

## Create configuration files
/root/.tarsnaprc:
```
cachedir /usr/local/tarsnap-cache
keyfile /root/tarsnap-susie.guksu.me
nodump
print-stats
checkpoint-bytes 1G
```

/root/tarsnapper.conf:
```
deltas: 7d 90d
target: $name-$date
jobs:
  mail:
    source: /var/vmail/
```

## Cron job
Finally create a cron job to run tarsnapper:
```
42 3 * * * tarsnapper -c /root/tarsnapper.conf make
```

# Various commands
## Create an archive
```
tarsnap -cvf <archivename> /etc/
```

## Create an archive using a different working directory
```
tarsnap -cvf <archivename> -C / etc/
```

## Extract an archive
```
cd /tmp
tarsnap -xvf <archivename>
tarsnap -xvf <archivename> <filename>
```

## List archive contents
```
tarsnap -tvf <archivename>
```

## Delete archive
```
tarsnap -dvf <archivename>
```

## Delete all archives
```
tarsnap --nuke
```

## Dry-runs
```
tarsnap –cvf complete-2014-12-28 --dry-run /
```

## List archives
```
tarsnap --list-archives -v | sort -ik2,3 | column -t
```

## Print statistics
```
tarsnap --print-stats
tarsnap --print-stats -f <archivename>
```

## Rebuild the directory
```
tarsnap --fsck
```
