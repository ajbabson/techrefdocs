## Git Notes

### Config files
.git/config -> Repository specific (git config --file (default if no option))
~/.gitconfig -> user specific (git config --global)
/etc/gitconfig -> system wide (git config --system)

```
git config -e --global
git config -l
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

`cat .git/config`<br>

`git diff --cached`<br>

`.git/info/exclude`<br>

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
Edit configuration options<br>
`git config -e --global`

Initialize empty repository in the current directory<br>
`git init .`

Add a file to the ignore list<br>
`echo "db.sqlite3" >> .gitignore`<br>

Helpful suggestions on this site<br>
`gitignore.io`<br>

Add the current directory to the repository<br>
`git add .`<br>
Add a single directory to the repository<br>
`git add <dir>`

Remove a file<br>
`git rm a_file.txt`<br>
`git commit -m "Removed a_file.txt"`

Rename<br>
`git mv`

Git rm -r recursively removes files from the working tree and from the index.
The --cached option is used to ask a command that usually works on files in
the working tree to only work with the index.<br>
`git rm -r --cached superlists/__pycache__`<br>

Check the commit status<br>
`git status`<br>

git branch (HEAD marked with \*)<br>
show all <br>
`git branch -a`<br>
show remotes<br>
`git branch -r`<br>
verbose<br>
`git branch -v`<br>
delete<br>
`git branch -d (-D force)`

Diff the modified files with the files in the repository<br>
`git diff`

Show the diff that you're about to commit<br>
`git diff --staged`

`git diff <commit number> <commit number>`<br>

Commit files to the repository<br>
`git commit`

Commit files and automatically add any changes to tracked files (i.e., any
files that we’ve committed before).  It won’t add any brand new files (you
have to explicitly git add them yourself)<br>
`git commit -a`

Commit and add message without entering edit mode<br>
`git commit -m "Message"`

amend last commit<br>
`git commit --amend`

List files<br>
`git ls-files`<br>
List files with objects<br>
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

graphical wrapper to git log<br>
`gitk --all`

`git gui`

`git commit -av`

```
git push
git push --set-upstream origin foo
git config --global push.default simple
```

`git commit --patch`

create a branch<br>
`git branch mybranch`

point your current branch to the new one<br>
`git checkout mybranch`

or in a single command<br>
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

remove a file from staged commit<br>
`git reset HEAD <filename>`

add a file to the previous commit<br>
`git commit --amend`

verify what was in last commit<br>
`git show --stat`

-t type of object (blob, tree, commit, tag)<br>
`git cat-file -t <hash>`

-p print<br>
`git cat-file -p <hash>`

`tree .git/refs`<br>
`less .git/packed-refs`

undo a merge
```
git revert
git reset
```
soft, mixed (default), hard

patch or force update of branch<br>
`git checkout [-p|-f]`

doesn't touch directories without -d, -x for ignored files<br>
`git clean -f`

interactive<br>
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


