# UEFI
Some notes:
- Currently most PC systems that use UEFI also have a so-called “Compatibility Support Module” (CSM) in the firmware, which provides exactly the same interfaces to an operating system as a classic PC BIOS, so that software written for the classic PC BIOS can be used unchanged.
- One major difference is the way the harddisk partitions are recorded on the harddisk. While the classic BIOS and UEFI in CSM mode use a DOS partition table, native UEFI uses a different partitioning scheme called “GUID Partition Table” (GPT).
- The other major difference between BIOS (or UEFI in CSM mode) and native UEFI is the location where boot code is stored and in which format it has to be. This means that different bootloaders are needed for each system.
- Booting from a disk with GPT is only possible in native UEFI mode.
- If you are using drives over 2TB (or plan to be using UEFI in future) you should be using GPT.
