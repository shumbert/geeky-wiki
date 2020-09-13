# Git
## Set up git on a new machine
```
# start ssh-agent if not running
eval $(ssh-agent)

# load your ssh key
ssh-add ~/.ssh/my-ssh-key

# Do some basic git config
git config --global user.email "__email_address__"
git config --global user.name "__name__"
git config --global core.excludesfile '~/.gitignore'
echo '.*.sw[po]' >> ~/.gitignore
```

## Untrack file
To stop tracking files which were previously checked in git apply the following commands:
```
vim .gitignore # add the file to .gitignore
git rm --cached /path/to/file
git commit -m 'some meaningful message'
git push
```

## Un-stage files
```
git reset HEAD -- path/to/file # unstage file
git reset HEAD -- .  # recursively unstage all files
```

## Remove sensitive data from git repos
**Note:** this will remove sensitive data from the master repo, however users local repositories may still have it. Best way to address the issue is to change your passwords/keys/whateveritis/...

Some links:
- [gitrob](https://github.com/michenriksen/gitrob/)
- [gitleaks](https://github.com/zricethezav/gitleaks)
- [Removing sensitive data from a repository](https://help.github.com/articles/removing-sensitive-data-from-a-repository/)
- [BFG](https://rtyley.github.io/bfg-repo-cleaner/)

Here is a quick how-to for BFG (you need to download the BFG jar and install java first):
```
git clone --mirror url/to/your/repo.git
echo '__my_password__' >> secret.txt
java -jar bfg.jar --replace-text secret.txt repo.git
cd repo.git # check history with git log and git diff
git reflog expire --expire=now --all && git gc --prune=now --aggressive
git push # you may have to unprotect the branch first
```

After rewriting the history users need to update their local repository:
```
git checkout -B branch origin/branch
```
