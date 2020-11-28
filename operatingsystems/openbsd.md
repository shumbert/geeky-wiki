# OpenBSD links
- [Firewalling with OpenBSD's PF packet filter](https://home.nuug.no/~peter/pf/en/)
- [OpenBSD (U)EFI bootloader howto](https://blog.jasper.la/openbsd-uefi-bootloader-howto.html)
- [OpenBSD and you](https://home.nuug.no/~peter/blug2016/)
- [OpenBSD Jumpstart](http://www.openbsdjumpstart.org/)
- [portroach - OpenBSD Ports Distfile Scanner ](https://portroach.openbsd.org/)
- [Why OpenBSD rocks - The facts](https://why-openbsd.rocks/fact/)
- [Writing Exploit-Resistant Code With OpenBSD](https://lteo.net/blog/2019/04/27/carolinacon-15-writing-exploit-resistant-code-with-openbsd/)
- [Package management in OpenBSD](https://unixsheikh.com/articles/package-management-in-openbsd.html)
- [Is OpenBSD Secure](https://isopenbsdsecu.re/)
- [OpenBSD handbook](https://www.openbsdhandbook.com/)
- [Setting up a WireGuard® client with routing domains on OpenBSD](https://codimd.laas.fr/s/NMc3qt5PQ#)
- [OpenBSD Router Guide](https://www.unixsheikh.com/tutorials/openbsd-router-guide/)

## Hardware support
- [OpenBSD on the Lenovo ThinkPad X1 Carbon (5th Gen)](https://jcs.org/2017/09/01/thinkpad_x1c#openbsd-support)
- [OpenBSD on the Lenovo ThinkPad X1 Carbon (7th Gen)](https://jcs.org/2019/08/14/x1c7)
- [An OpenBSD Workstation](http://eradman.com/posts/openbsd-workstation.html)
- [OpenBSD on a laptop](https://www.c0ffee.net/blog/openbsd-on-a-laptop/)

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
