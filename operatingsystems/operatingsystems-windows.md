# Windows XP
## List component services in each process
```
tasklist /svc
```

# Shrink Windows VM virtual hard drive
## Disk clean up (guest)
Open the disk clean up utility, select clean system files and make sure Windows updates are selected. On older Windows version you may have to install an [update](https://support.microsoft.com/en-us/help/2852386/disk-cleanup-wizard-addon-lets-users-delete-outdated-windows-updates-o) to get the Windows updates clean up option.

## Zero out free disk space (guest)
Use [SDelete](https://docs.microsoft.com/en-us/sysinternals/downloads/sdelete) to zero out free space:
```
cmd> sdelete64.exe -z C:
```

## Compact the virtual hard drive (host)
Shut down the guest then use the following command to compact the virtual drive:
```
VBoxManage modifymedium disk <filename> --compact
```

# Windows 10
## Windows Subsystem for Linux
First activate it, open Powershell as administrator and type:
```
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

Then open Microsoft Store and install one of the Linux distributions.

Windows drive is mounted under /mnt/.

## Useful shortcuts
| Keys | Shortcut |
|---|---|
| Windows key + L | Lock your PC |
| F10 |	Activate the Menu bar in the active app |
| Windows key + A | Open Action center |
| Windows key + E | Open File Explorer |
| Windows key + I | Open Settings |
| Windows key + R | Open the Run dialog box |
| Windows key + S | Open search |
| Windows key + period (.) or semicolon (;) | Open emoji panel |
| Windows key + Pause | Display the System Properties dialog box |
| | |
| Windows key + number | Open the desktop and start the app pinned to the taskbar in the position indicated by the number. If the app is already running, switch to that app |
| Windows key + Shift + number | Open the desktop and start a new instance of the app pinned to the taskbar in the position indicated by the number |
| Windows key + Ctrl + number | Open the desktop and switch to the last active window of the app pinned to the taskbar in the position indicated by the number |
| Windows key + Alt + number | Open the desktop and open the Jump List for the app pinned to the taskbar in the position indicated by the number |
| Windows key + Ctrl + Shift + number |	Open the desktop and open a new instance of the app located at the given position on the taskbar as an administrator |
| | |
| Windows key + Up arrow | Maximize the window |
| Windows key + Down arrow | Remove current app from screen or minimize the desktop window |
| Windows key + Left arrow | Maximize the app or desktop window to the left side of the screen |
| Windows key + Right arrow | Maximize the app or desktop window to the right side of the screen |
| Windows key + Home | Minimize all except the active desktop window (restores all windows on second stroke) |
| Windows key + Shift + Up arrow | Stretch the desktop window to the top and bottom of the screen |
| Windows key + Shift + Down arrow | Restore/minimize active desktop windows vertically, maintaining width |
| Windows key + Shift + Left arrow or Right arrow | Move an app or window in the desktop from one monitor to another |
| | |
| Windows key + Tab | Open Task view |
| Windows key + Ctrl + D | Add a virtual desktop |
| Windows key + Ctrl + Right arrow | Switch between virtual desktops you’ve created on the right |
| Windows key + Ctrl + Left arrow | Switch between virtual desktops you’ve created on the left |
| Windows key + Ctrl + F4 | Close the virtual desktop you're using |
| | |
| Shift + click a taskbar button | Open an app or quickly open another instance of an app |
| Ctrl + Shift + click a taskbar button | Open an app as an administrator |
| Ctrl + click a grouped taskbar button | Cycle through the windows of the group |