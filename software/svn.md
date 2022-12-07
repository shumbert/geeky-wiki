# SVN Revisions
SVN revision numbers apply to the entire repository tree, however in your working copy it's common to have a mixture of revisions. Reason being when you commit an update only files that you changed have their revision number bumped, other files and directories revision doesn't change.

Let's say you checkout an SVN repository with the following content (and their associated revision numbers):
```
4 .
4 hello.txt
4 goodbye.txt
```

You update and commit hello.txt, now revision numbers in your working copy look like:
```
4 .
5 hello.txt
4 goodbye.txt
```

But now if you run `svn update` revision numbers look like:
```
5 .
5 hello.txt
5 goodbye.txt
```

This is also the reason why `svn log` may not show your latest commits. `svn log` essentially means `svn log .`, and revision number for `.` is not dump until you `svn update`.

# Update your working copy
```
svn update
svn status --verbose # show revision number for each file and directory
svn status --verbose --update # contact the server to show any pending changes
svn update -r 1729 # Make the current directory look like it did in r1729
```

# Revert changes
```
svn revert # Restore a file or directory to its unmodified state
           # You can also use to undo scheduled operation (such as file deletion or move)
```

# Diffing
```
svn diff # show local changes
svn diff -r 3 rules.txt # show diff between working copy and a specific revision number
svn diff -r 2:3 rules.txt # show diff between two revision numbers
svn diff -c 3 rules.txt # compare revision passed in argument with previous revision
```

# Show logs
```
svn log
svn log -diff # append a diff to each log chunk
```

# Show older versions of files
```
svn cat -r 2 rules.txt
```

# SVN blame
```
svn annotate rules.txt
svn blame rules.txt
```
