# Run cinnamon in a VM
In Settings > Display:
- change graphic controller to VMSVGA
- enable 3D acceleration

# Themes & Icons
- create directories ~/.icons and ~/.themes
- download CBlack.zip from from https://cinnamon-spices.linuxmint.com/themes/view/CBlack and extract it under ~/.themes
- clone or download mint-y icons from https://github.com/linuxmint/mint-y-icons, copy everything under usr/share/icons to ~/.icons
- in Settings > Themes, select Mint-Y Orange for Icons and C-Black for everything else

# Cinnamon settings
- System settings > Windows > Behaviour > Windows focus mode: sloppy
- System settings > Effects: disable everything

# Some shortcuts
| Shortcut | Keys |
|---|---|
| Show the window selection screen | Ctrl+Alt+Down |
| Show the workspace selection screen | Ctrl+Alt+Up |
| Show desktop | Super+D |
| Close window | Alt+F4 |
| Activate window menu | Alt+Space |
| Toggle Maximization state | Alt+F10 |
| Resize window | Alt+F8 |
| Tile | Super+Top/Bottom/Left/Rigt |
| Snap | Ctrl+Super+Top/Bottom/Left/Rigt |
| Move window to left workspace | Shift+Ctrl+Alt+Left |
| Move window to right workspace | Shift+Ctrl+Alt+Right |
| Move window to left monitor | Shift+Super+Left |
| Move window to right monitor | Shift+Super+Right |
| Switch to left workspace | Ctrl+Alt+Left |
| Take screenshot of area | Shift+Print |
| Copy a screenshot of an area to clipboard | Ctrl+Shift+Print |
| Launch terminal | Ctrl+Alt+T |

**Note:** you can resize windows with Alt+Right click

**Note:** a snapped window will be considered part of the screen real estate, and maximized windows will avoid snapped windows.  Tiled windows (unmodified) are treated just as before – they are ‘stuck’ to the screen edge, but don’t receive any special treatment.

You can export keyboard shortcut keys:
```
dconf dump /org/cinnamon/desktop/keybindings/ >keybindings-backup.dconf
```

Then re-import:
```
dconf load /org/cinnamon/desktop/keybindings/ <keybindings-backup.dconf
```