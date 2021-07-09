# Links
- [Visual Studio Code - Keyboard shortcuts for Linux](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-linux.pdf)
- [Visual Studio Marketplace - Sort lines](https://marketplace.visualstudio.com/items?itemName=Tyriar.sort-lines)

# Extensions
- Bash Debug
- Bash IDE
- Docker
- Go
- Python
- shellcheck

# Useful shortcuts
| Keys | Command | Comment |
|---|---|---|
| Ctrl+Shift+Alt+Up | Copy line up | |
| Ctrl+Shift+Alt+Down | Copy line down | |
| Alt+Up | Move line up | |
| Alt+Down | Move line down | |
| Ctrl+Shift+O | Go to symbol in file | |
| Ctrl+T | Go to symbol in marketplace | |
| Ctrl+G | Navigate to specific line | |
| Ctrl+K Ctrl+X | Trim trailing whitespaces | |
| Ctrl+Shift+[ | Fold region | |
| Ctrl+Shift+] | Unfold region | |
| Ctrl+K Ctrl+0 | Fold all regions | |
| Ctrl+K Ctrl+J | Unfold all regions | |
| Ctrl+K Ctrl+/ | Fold all block comments | |
| Ctrl+L | Select current line | |
| Ctrl+Home | Navigate to beginning of file | |
| Ctrl+End | Navigate to end of file | |
| Ctrl+Space | Open IntelliSense suggestions widget | |
| F2 | Rename symbol | |
| F12 | Go to symbol definition | |
| Ctrl+Shift+G | Git integration | |
| Ctrl+P | search for files or symbols (type @\<symbol name\> for symbol search) | |
| Ctrl+Shift+P | open command palette | |
| Ctrl+, | edit settings | |
| Ctrl+PageDown | go to the right editor | |
| Ctrl+PageUp | go to the left editor | |
| Ctrl+Tab | open the previous editor in the editor group MRU list | |
| Ctrl+1 | go to the leftmost editor group | |
| Ctrl+2 | go to the center editor group | |
| Ctrl+3 | go to the rightmost editor group | |
| Ctrl+W | close the active editor | |
| Ctrl+K W | close all editors in the editor group | |
| Ctrl+K Ctrl+W | close all editors | |

# Files
Linux - Delete $HOME/.config/Code and ~/.vscode.


The workspace settings file is located under the .vscode folder in your root folder.

# Tips and tricks
- You can add vertical column rulers to the editor with the editor.rulers setting, which takes an array of column character positions where you'd like vertical rulers.
- Besides searching and replacing expressions, you can also search and reuse parts of what was matched, using regular expressions with capturing groups. Enable regular expressions in the search box by clicking the Use Regular Expression .* button (Alt+R) and then write a regular expression and use parenthesis to define groups. You can then reuse the content matched in each group by using $1, $2, etc. in the Replace field.
- You can open as many editors as you like side by side vertically and horizontally. If you already have one editor open, there are multiple ways of opening another editor to the side of the existing one:
  - Alt click on a file in the Explorer.
  - Ctrl+\ to split the active editor into two.
  - Open to the Side (Ctrl+Enter) from the Explorer context menu on a file.
  - Click the Split Editor button in the upper right of an editor.
  - Drag and drop a file to any side of the editor region.
  - Ctrl+Enter (macOS: Cmd+Enter) in the Quick Open (Ctrl+P) file list.
- If you want to run a command-line tool in the context of the folder you currently have open in VS Code, right-click the folder and select Open in Command Prompt (or Open in Terminal on macOS or Linux).
- By default, VS Code excludes some folders from the Explorer (for example. .git). Use the files.exclude setting to configure rules for hiding files and folders from the Explorer.
- If you select two items, you can now use the context menu Compare Selected command to quickly diff two files.
- In settings, enter @modified in the search field to see all modified options
- When you single-click or select a file in the Explorer, it is shown in a preview mode (indicated by italics in the Tab heading) and reuses an existing Tab. This is useful if you are quickly browsing files and don't want every visited file to have its own Tab. When you start editing the file or use double-click to open the file from the Explorer, a new Tab is dedicated to that file.
- To customize your editor by language, run the global command Preferences: Configure Language Specific Settings (command id: workbench.action.configureLanguageBasedSettings) from the Command Palette (Ctrl+Shift+P) which opens the language picker. Selecting the language you want, opens the Settings editor with the language entry where you can add applicable settings.

## Git integration
- Review pane: navigate through diffs with F7 and Shift+F7. This will present them in a unified patch format. Lines can be navigated with arrow keys and pressing Enter will jump back in the diff editor and the selected line.
- Stage selected: Stage a portion of a file by selecting that file (using the arrows) and then choosing Stage Selected Ranges from the Command Palette.

## Editors

# Markdown
| Keys | Command | Comment |
|---|---|---|
| Ctrl+Shift+V | preview markdown file | |
| Ctrl+K V | open markdown edit and preview side by side | |

# Python
- Run Selection/Line in Python Terminal command (Shift+Enter) is a simple way to take whatever code is selected, or the code on the current line if there is no selection, and run it in the Python Terminal. An identical Run Selection/Line in Python Terminal command is also available on the context menu for a selection in the editor.

# Golang
TODO
