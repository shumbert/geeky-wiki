# Some links
- [Firefox support](https://support.mozilla.org/en-US/)
- [Bookmarks in Firefox](https://support.mozilla.org/en-US/kb/bookmarks-firefox<Paste>)
- [Keyboard shortcuts - Perform common Firefox tasks quickly](https://support.mozilla.org/en-US/kb/keyboard-shortcuts-perform-firefox-tasks-quickly)
- [Address bar autocomplete in Firefox](https://support.mozilla.org/en-US/kb/address-bar-autocomplete-firefox)
- [Restore bookmarks from backup or move them to another computer](https://support.mozilla.org/en-US/kb/restore-bookmarks-from-backup-or-move-them)
- [Bookmark Tags - Categorize bookmarks to make them easy to find](https://support.mozilla.org/en-US/kb/categorizing-bookmarks-make-them-easy-to-find)

# Some useful shortuts
| Shortcut | Command |
|---|---|
| Ctrl + L | Focus Address Bar |
| Ctrl + J | Focus Address Bar for web searches |
| Ctrl + U | Page Source |
| Ctrl + I | Page Info |
| Ctrl + Shift + A | Add-ons |
| Ctrl + Shift + O | Show the Library (bookmarks) |
| Alt + ↓/↑ | Switch search engine (after you have written something in the address bar |

# Address Bar
By default, when you type something in the address bar it will display matches and suggestions from a variety of source: default search engine, history, bookmarks, open tabs, ...

If you are looking for a specific type of results you can use of the special characters below (followed by space):
- ^ for browsing history
- \* for bookmarks
- \+ for tagged bookmarks
- % for open tabs
- ? for search engine suggestions

# Bookmarks
Firefox automatically backup your bookmarks and saves up to 15 backups in the profile bookmarkbackups folder.

You can manually backup and restore bookmakrs. But **caution** restoring bookmarks from a backup will overwrite your current set of bookmarks with the ones in the backup file.

# Run latest Firefox on Debian
You can download the latest Firefox tarball directly from Mozilla and install it somewhere in your home folder:
```
wget -O firefox.tar.bz2 "https://download.mozilla.org/?product=firefox-latest&os=linux64&lang=en-US"
mkdir $HOME/mozilla/
tar xjf firefoxsetup.tar.bz2 -C $HOME/mozilla/
```

**note:** if you install Firefox in a directory where you don't have write permissions, auto-updates won't work

# Profiles vs Containers
Firefox profiles are equivalent to Chrome profiles. There is no built-in UI to switch between profiles though, so it requires more work. To manage profiles open a new tab and go to:
```
about:profiles
```

You can run multiple instances of firefox with different profiles. Start the instances this way:
```
firefox -no-remote -p profile1
firefox -no-remote -p profile2
```

You also have the option to use container tabs within a given profile. Container tabs have distinct browser storage (cookies and site data) from other containers. You can use them to log in multiple times in a single website, or to avoid tracking cookies following you between websites. To manage container tabs install the Firefox Multi-Account Containers extension.

Note that container tabs are disabled in Private Browsing and when Never Remember History is selected in your privacy preferences.

Some links:
- https://wiki.mozilla.org/Security/Contextual_Identity_Project/Containers
- https://support.mozilla.org/en-US/kb/containers
