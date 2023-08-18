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
git config --global alias.b 'branch'
git config --global alias.ba 'branch -a'
git config --global alias.st 'status -sb'
git config --global --unset alias.unset_me
git config --global alias.show-graph 'log --graph --abbrev-commit --pretty=oneline'
```

### Other
Edit configuration options<br>
`git config -e --global`

Helpful suggestions on this site<br>
`gitignore.io`<br>

Git rm -r recursively removes files from the working tree and from the index.
The --cached option is used to ask a command that usually works on files in
the working tree to only work with the index.<br>
`git rm -r --cached superlists/__pycache__`<br>

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

Commit files and automatically add any changes to tracked files (i.e., any
files that we’ve committed before).  It won’t add any brand new files (you
have to explicitly git add them yourself)<br>
`git commit -a`

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

```
git push --set-upstream origin foo
git config --global push.default simple
```

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

Create your SSH keys:

`ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`

Add your SSH keys:

Click your user icon at the top right of the screen and select Settings.

On the left side menu select SSH and GPG keys.

Select New SSH Key and add follow the instructions to add your key.

Test your SSH access with the key:

```
$ ssh -i ~/.ssh/id_rsa -T git@github.com
Hi <your username> ! You've successfully authenticated, but GitHub does not provide shell access
```


