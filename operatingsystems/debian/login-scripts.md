All the stuff below is from [here](https://www.sitepoint.com/understanding-nix-login-scripts/).

# Login shells
System-wide login shell init file is /etc/profile. It is meant to be readable by all shells to it's POSIX compliant.

User files are:
- ~/.profile (sh, dash)
- ~/.bash_profile, ~/.bash_login and ~/.profile (bash, read in that order)

Theory was that generic shell initialization stuff would go to ~/.profile, and bash specific initialization stuff would go to ~/.bash_profile. In practice most linux users use bash, and just juse ~/.profile.

# Non-login shells
When started as an interactive non login shells, bash reads /etc/bash.bashrc and ~/.bashrc (in that order).

# X sessions
## xsessionrc
when an X window session is started (either via display manager or startx) /etc/X11/Xsession is executed. /etc/X11/Xsession sources files from /etc/X11/Xsession.d/.

Debian includes a file named /etc/X11/Xsession.d/40x11-common_xsessionrc, it checks if ~/.xsessionrc is readable and sources it. ~/.xsessionrc is a perfect place to load environment variables or run utilities at launch.

Some display managers (such as gdm) source /etc/profile and ~/.profile, others (such as lightdm) do not. You can use ~/.xsessionrc to source /etc/profile and ~/.profile.

**Note:** ~/.xsessionrc only exists in debian and its derivatives.

## xsession
/etc/X11/Xsession.d/50x11-common_determine-startup determines the session manager to load. If ~/.xsession exists and is executable, it will be saved and executed later as part of 99x11-common_start.

For instance:
```
exec x-session-manager
```

Since ~/.xsession is meant for running the session manager, the X session will log out and you will be returned to your display manager when this script terminates.