[pass](https://www.passwordstore.org/) is the standard unix password manager.

# install pass
```
sudo apt install pass pass-extension-tail qtpass
```

**Note:** the debian package pass-extension-tail does not include the bash completion file. Download it from the [repo](https://github.com/palortoff/pass-extension-tail) then copy it to /etc/bash_completion.d/.

# cheatsheet
```
# init pass (first create a gpg key)
pass init <keyid>

# add a password file (generate the password)
pass generate Email/jasondonenfeld.com 15

# add a password file (password provided by the user)
pass insert Business/cheese-whiz-factory

# list password files
pass show

# print a password
pass show Business/cheese-whiz-factory

# copy a password to clipboard
# by default it only copies the first line of the password file
pass show -c Business/cheese-whiz-factory

# print additional inforamtion (print password file except the first line)
pass tail <password file>

# move a password file around
pass mv old_path new_path

# remove a password file
pass rm Business/cheese-whiz-factory

# edit a password file
pass edit Business/cheese-whiz-factory

# git - init
pass git init

# git - add a remote
pass git remote add origin git@server:repo.git

# git - initial commit
pass git push -u --all

# git - subsequent commits (each modification is a commit)
pass git push
pass git pull

# edit additional information
pass tailedit <password file>
```

# set up pass on a new machine
1. import the gpg key
```
gpg --output key.gpg --armor --export-secret-keys <key-id> # on the old machine
gpg --impport key.gpg # on the new machine
```
2. install pass
3. clone the repo
```
git clone git@server:repo.git $HOME/.password-store
```

# some notes
- Using pass passwords and other information are encrypted, however names of folders and password files are not, revealing which accounts you have passwords for. There is an extension addressing this issue: pass-tomb. However pass-tomb is not compatible with the git feature.

# passmenu
There is a [dmenu script](https://git.zx2c4.com/password-store/tree/contrib/dmenu/passmenu) for pass.

# qtpass
[qtpass](https://qtpass.org/) is a GUI for pass.

Configure qtpass:
- Settings
  - always copy to clipboard
  - autoclear after 60 seconds
  - hide password in content panel
  - autoclear panel after 60 seconds
  - use git
- Template
  - use default template (login+url)

# Issues
If you get an error "there is no assurance this key belongs to the named user" when creating a new entry, you may have to manually set the trust level for the gpg key:
```
gpg --edit-key xxxxxx
gpg> trust
? 5
gpg> save
```

Then if you get an error "public key of ultimately trusted key 00000000 not found" you may have to manually fix the trust database:
```
gpg --export-ownertrust > ownertrust-gpg.txt
mv ~/.gnupg/trustdb.gpg ~/.gnupg/trustdb.gpg-broken
vim ownertrust-gpg.txt # Removes the key gpg is complaining about
gpg --import-ownertrust ownertrust-gpg.txt
```
