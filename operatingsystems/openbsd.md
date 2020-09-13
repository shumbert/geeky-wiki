# Non-free firmwares
Use fw_update to download and install firmware packages for various drivers:
```
fw_update -a
```

# Ports
## Links
- [OpenBSD porting workshop #1: Porting basics](https://www.youtube.com/watch?v=z_TnemhzbXQ)

## Files and Directories
- /usr/ports/mystuff/: special directory for port development
- /usr/ports/infrastructure/templates/Makefile.template: Makefile template
- /usr/ports/infrastructure/bin/portcheck: lint-ish script for OpenBSD ports

## Make sub-commands
```
make fetch # grab the source archive
make makesum # download the source archive and create the distinfo file (tarball hash and size)
make show=DISTNAME # show variables
make show=WRKDIR
make configure # configure the port
make build # build the port
make fake # install files to fake root (WRKDIR)
make plist # make plist
make port-lib-depends-check
make package # build the package
make install # install the package
```

## Package description
Package description file have to be created manually: pkg/DESCR.

Cut lines at 72 characters:
```
fmt -72 D
```

## Patches
Go to source directory, copy the file to update and then edit it
```
cd $(make show=WRKSRC)
cp README README.orig
vi README
```

Go back to port directory and create the patch file (directory patches/ will be automatically created):
```
cd -
make update-patches # add a comment at the top
```
