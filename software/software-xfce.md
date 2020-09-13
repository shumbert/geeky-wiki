# Backup and restore your XFCE settings
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