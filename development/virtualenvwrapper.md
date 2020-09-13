# Installation (Debian)
```
sudo apt install virtualenvwrapper
```

Add those lines in your shell configuration file:
```
WORKON_HOME=$HOME/.virtualenvs
source /usr/share/virtualenvwrapper/virtualenvwrapper.sh
```

# Cheatsheet
## List environments
```
workon
```

## Create an environment
```
mkvirtualenv env1
mkvirtualenv --python=$(which python3) env2
```

## Switch to another environment
```
workon env2
```
