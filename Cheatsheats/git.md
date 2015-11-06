# Git Cheatsheet

#### Initialize a folder to be a git repository

```
git init
```

#### Connect a git repo folder to a github repository
```
git remote add origin git@github.com:github-name/repository-name.git
``` 

#### Saving your changes to your git repository

```
git add .
git commit -m "message about changes"
```

#### Pushing local changes up to Github

```
git push origin master
```

## Some more git commands

```
#see which files need to be added/commited
#and see whether you are up to date with your remote
git status

#see the history of changes
git log

#see all of your changes (before you git add)
git diff

#basically unadd
git reset

#do away with your changes
git checkout [filename]

#remove a file and let git know
git rm [filename]

#move a file and let git know
git mv [orig_file] [new_file]
```