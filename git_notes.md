## Git Notes

### Config files
.git/config -> Repository specific (git config --file (default if no option))
~/.gitconfig -> user specific (git config --global)
/etc/gitconfig -> system wide (git config --system)

```
git config -e --global
git config -l
git config --global user.name "Aric Babson"
git config --global user.email "aricb@protonmail.com"
```

`cat .git/config`

`git diff --cached`

`.git/info/exclude`

### aliases
```
git config --global alias.lg 'log --graph --oneline --decorate'
git config --global alias.lga 'log --graph --oneline --decorate --all'
git config --global alias.ci 'commit'
git config --global alias.co 'checkout'
git config --global alias.st 'status -sb'
git config --global --unset alias.foo
git config --global alias.show-graph 'log --graph --abbrev-commit --pretty=oneline'
```

### Other
Edit configuration options
`git config -e --global`

Initialize empty repository in the current directory
`git init .`

Add a file to the ignore list
`echo "db.sqlite3" >> .gitignore`

Helpful suggestions on this site
`gitignore.io`

Add the current directory to the repository
`git add .`
Add a single directory to the repository
`git add <dir>`

Remove a file
`git rm a_file.txt`
`git commit -m "Removed a_file.txt"`

Rename
`git mv`

Git rm -r recursively removes files from the working tree and from the index.
The --cached option is used to ask a command that usually works on files in
the working tree to only work with the index.
`git rm -r --cached superlists/__pycache__`

Check the commit status
`git status`

git branch (HEAD marked with \*)
show all 
`git branch -a`
show remotes
`git branch -r`
verbose
`git branch -v`
delete
`git branch -d (-D force)`

Diff the modified files with the files in the repository
`git diff`

Show the diff that you're about to commit
`git diff --staged`

`git diff <commit number> <commit number>`

Commit files to the repository
`git commit`

Commit files and automatically add any changes to tracked files (i.e., any
files that we’ve committed before).  It won’t add any brand new files (you
have to explicitly git add them yourself)
`git commit -a

Commit and add message without entering edit mode
`git commit -m "Message"`

amend last commit
`git commit --amend`

List files
`git ls-files`
List files with objects
`git ls-files -s`

Show the log
```
git log
git log --oneline
git log --oneline --graph --decorate --all
git show <SHA>
git show (defaults to HEAD)
git show master (or other branch)
```
Show log details (includes diff)
`git show 9d156dfad0f2932ec48c747bbdf592385c419143` (commit number)
(without commit number shows most recent)

graphical wrapper to git log
`gitk --all`

`git gui`

`git commit -av`

```
git push
git push --set-upstream origin foo
git config --global push.default simple
```

`git commit --patch`

create a branch
`git branch mybranch`
point your current branch to the new one
`git checkout mybranch`
or in a single command
`git checkout -b mybranch`

`git cherry-pick <SHA>`

```
git remote
git remote -v
git remote add {name} {url}
git remote rm {name}
```

updating your branch with remote
```
git fetch
git pull
git pull --rebase [--no-rebase]
git config --global pull.rebase true
```

remove a file from staged commit
`git reset HEAD <filename>`

add a file to the previous commit
`git commit --amend`
verify what was in last commit
`git show --stat`

-t type of object (blob, tree, commit, tag)
`git cat-file -t <hash>`
-p print
`git cat-file -p <hash>`

`tree .git/refs`
`less .git/packed-refs`

undo a merge
```
git revert
git reset
```
soft, mixed (default), hard

patch or force update of branch
`git checkout [-p|-f]`
doesn't touch directories without -d, -x for ignored files
`git clean -f`
interactive
`git clean -idx`

### Git for Windows
https://git-for-windows.github.io/

install with git bash only option and defaults for the rest

Create your SSH keys

`ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`

Add your SSH keys

Click your user icon at the top right of the screen and select Settings.

On the left side menu select SSH and GPG keys.

Select New SSH Key and add follow the instructions to add your key.

Test your SSH access with the key:

```
$ ssh -i ~/.ssh/id_rsa -T git@github.com
Hi <your username> ! You've successfully authenticated, but GitHub does not provide shell access
```

Clone a repository

At bottom left under Organization settings, select arkadin-nio.

Once on the arkadin-nio page, select Repositories.

Select git-playground.

```
$ git clone https://github.com/my_org/git-playground.git
Cloning into 'git-playground'...
Username for 'https://github.com': ababson
Password for 'https://ababson@github.com': 
remote: Counting objects: 27, done.
remote: Compressing objects: 100% (20/20), done.
remote: Total 27 (delta 5), reused 20 (delta 3), pack-reused 0
Unpacking objects: 100% (27/27), done.
Checking connectivity... done.
aric@sasquatch:~/CODE/$ ls
git-playground
aric@sasquatch:~/CODE/$ ls git-playground/
k-git-commands.txt  my-great-thing.py  README.md
```


