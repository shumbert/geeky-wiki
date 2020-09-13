# Run latest Firefox on Debian
You can download the latest Firefox tarball directly from Mozilla and install it under /opt/:
```
wget -O firefox.tar.bz2 "https://download.mozilla.org/?product=firefox-latest&os=linux64&lang=en-US"
sudo tar xjf firefoxsetup.tar.bz2 -C /opt/
```

The auto-update feature doesn't seem to work. Just repeat the instructions above when a new version is released.

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

# Settings
## block notifications
- Preferences
- Privacy & Security
- Permissions > Notifications > Settings
- Block new requests asking to allow notifications

## block websites from automatically playing sounds
- Preferences
- Privacy & Security
- Permissions
- check Block websites from automatically playing sounds

## disable search suggestions
- Preferences
- Search
- Default Search Engine
- uncheck Provide search suggestions

## no open tabs suggestions
- Preferences
- Privacy & Security
- Address Bar
- uncheck Open Tabs

## restore previous session
- Preferences
- General
- Startup
- check Restore previous session

## no logins & passwords
- Preferences
- Privacy & Security
- Logins & Passwords
- uncheck Ask to save logins and passwords for websites

## custom content blocking
- Preferences
- Privacy & Security
- Content Blocking
- check Custom
- block trackers in all windows
- block cookies: third-party trackers (or all third-party cookies)

## do not track
- Preferences
- Privacy & Security
- Content Blocking
- check Always send websites a "Do Not Track" signal

## delete cookies when firefox is closed
- Preferences
- Privacy & Security
- Cookies and Site Data
- check Delete cookies and site data when Firefox is closed

# Profiles
## browse profile
- extensions:
  - TreeStyleTabs
  - uBlock Origin
  - Page Translator Revised
- settings:
  - delete cookies when firefox is closed
  - block notifications
  - block websites from automatically playing sounds
  - disable search suggestions
  - no open tabs suggestions
  - no logins & passwords
  - custom content blocking
  - do not track
- sync:
  - bookmarks, add-ons and preferences

## personal profile
- extensions:
  - lastpass
  - Firefox Multi-Account Containers
  - uBlock Origin
  - Page Translator Revised
- containers:
  - google
  - banking
  - shopping
- settings:
  - block notifications
  - block websites from automatically playing sounds
  - disable search suggestions
  - no open tabs suggestions
  - restore previous session
  - no logins & passwords
  - do not track
- sync (optional, requires a different firefox account):
  - bookmarks, add-ons and preferences
