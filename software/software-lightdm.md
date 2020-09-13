# Bash profile
By default lightdm do not read your bash .profile when opening a new session. Any configuration from .profile (such as adding $HOME/.local/bin/ to $PATH) is not added. Create the file $HOME/.xsessionrc to address this:
```
if [ -r $HOME/.profile ]; then
    . $HOME/.profile
fi
```

# Virtualbox resizing display
If lightdm greeter does not automatically resize after installing virtualgox guest additions, add the following to /etc/lightdm/lightdm.conf:
```
[Seat:*]
greeter-setup-script=VBoxClient --vmsvga-x11
```