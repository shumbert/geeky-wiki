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

# Ugly fonts on Windows 10
Enable ClearType fonts by executing cttune.exe from Win+R, and then following on-screen instructions.

# Privacy and Security
## Encrypted Client Hello
Firefox supports [Encrypted Client Hello (ECH)](https://blog.mozilla.org/security/2021/01/07/encrypted-client-hello-the-future-of-esni-in-firefox/) since version 85. A few notes:
- Work started on Encrypted SNI but it turned out to only have incomplete protection, now development has shifted to ECH.
- With ECH the ClientHello is encrypted under the server's public key. The server's public key, used only for the purpose of encrypting the TLS handshake, is stored in a DNS record. More details [here](https://blog.cloudflare.com/encrypted-client-hello/).
- Even though the TLS handshake is now encrypted, the DNS query the client uses to retrieve the public key leaks information. So ECH is only meant to be used in combination with DoH.
- ECH in Firefox is not enabled by default, you can enable it via about:config.

## Supercookie protection
Firefox 85 and later has [supercookie protection](https://blog.mozilla.org/security/2021/01/26/supercookie-protections/). Essentially supercookies is trackers storing user identifiters in obscure parts of the browser like Flash Storage, ETags, HSTS flags, ...

With supercookie protection Firefox partitions a number of caches and network connections per top-level site.

## Total cookie protection
Firefox 86 and later has [total cookie protection](https://blog.mozilla.org/security/2021/02/23/total-cookie-protection/). Typically cookies can be shared between web sites, allowing trackers to "tag" your browser and follow you between websites. Now Firefox maintains a separate cookie jar for each website.

Total cookie protection is available when Enhanced Tracking Protection (ETP) is set to Strict Mode, and since Firefox 89 in [Private Browsing mode](https://blog.mozilla.org/security/2021/06/01/total-cookie-protection-in-private-browsing/).

## Smart Block
Firefox includes a tracking blocking feature which blocks third-party scripts and contents, but when activated it may interfere with websites normal behaviour as well as 3rd party login. To avoid this problem Firefox introduced SmartBlock which provides [local stand-ins scripts](https://blog.mozilla.org/security/2021/03/23/introducing-smartblock/) or quickly [unblocks scripts](https://blog.mozilla.org/security/2021/07/13/smartblock-v2/) when 3rd party login is needed.

## Site Isolation
Before Site Isolation Firefox would spawn one parent/privileged process which then launches and coordinates a number of child processes, mostly web content processes and utility processes. Although that architecture provides some level of protection an attacker could execute a sophisticated attack where a malicious site would gain full access to a web content process memory and potentially steal information stored by other web sites. More informatiton [here](https://hacks.mozilla.org/2021/05/introducing-firefox-new-site-isolation-security-architecture/).

Site Isolation has been rolled out in Firefox 94, now each web site is loading in a separate process.
