# Configuration
Xfce uses [xfconf](https://docs.xfce.org/xfce/xfconf/start) to manage its configuration: Xfconf is a hierarchical (tree-like) configuration system where the immediate child nodes of the root are called "channels". All settings beneath the channel nodes are called "properties".

Some useful commands:
```
# list all properties and their values in channel xfce4-desktop
xfconf-query -c xfce4-desktop -l -v

# hide panel 2
xfconf-query -c xfce4-panel -p /panels -t int -s 1 -a

# restore panel 2
xfconf-query -c xfce4-panel -p /panels -t int -s 2 -t int -s 1 -a

# reload xfce4-panel after changing properties
xfce4-panel -r
```

You can use those two scripts to create an xfce configuration:
- [install-xfce4](../files/install-xfce4)
- [configure-xfce4](../files/configure-xfce4): run this after launching xfce

**Note:** xfconf can be used to managed individual properties, but afaik you cannot use to bootstrap a default configuration. This is too bad, it would be interesting to have a single provisioning script which would install packages, then use xfconf to 1) bootstrap a default config, and 2) change the few settings you are insterested in.

## Backup and restore your XFCE settings
To backup your XFCE config backup those directories:
- $HOME/.config/xfce4
- $HOME/.local/share/xfce4
- $HOME/.config/Thunar

**Note:** not tested myself but it's recommended to log out from your graphical session before backing up your config. Then log back in with a different user (or via a terminal, or via ssh, ...) to copy the files.

To restore your config just untar the backup (make sure file ownership is correct though).

# Shortcuts
| Keys | Shortcut |
|---|---|
| Alt+F2 | application finder |
| Alt+F8 | resize window |
| Alt+F10 | maximize window |
|||
| Ctrl+Alt+Home | move window to previous workspace |
| Ctrl+Alt+End | move window to next workspace |
| Ctrl+Alt+1 | move window to workspace 1 |
| Ctrl+Alt+2 | move window to workspace 2 |
|||
| Ctrl+Super+Up | Tile up |
| Ctrl+Super+Down | Tile down |
| Ctrl+Super+Left | Tile left |
| Ctrl+Super+Right | Tile right |
