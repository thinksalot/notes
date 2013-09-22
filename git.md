Git reference
===

### Index
Index is a staging area between working tree and the repository.

Index contains a list of files that will be added to the repository if you run `git commit` command next.

Running `git status` displays the contents of the index.

Before we commit files to the repository, we need to add files to the index using `git add`

When we run `git status` we see a list of files in three categories:

* Files that have been added to the index (**staged**,by using `git add`)

* Files that are tracked but not added to index.

* Files that are completely untracked.

[[gitguys]](http://www.gitguys.com/topics/whats-the-deal-with-the-git-index/)
[[git-scm]](http://git-scm.com/book/en/Git-Basics-Recording-Changes-to-the-Repository)

Git commands
===

### Undo (uncommitted) changes to tracked files:
`git reset --hard` discard all changes to working directory

`git checkout -- file.txt` discards changes to `file.txt` only

`git checkout -- *` discards all changes to working directory

### Undo (committed) changes to tracked files:
`git reset --soft HEAD~1` 

Resets the `HEAD` to secondlast commit (specified here by `HEAD~1`)

`--soft` means to leave the changed files untouched. 

Using `--hard ` instead removes the changes in file aswell (ie modifies index).

### Remove untracked files and directories:
`git clean -fd` - `d` flag removes untracked directories in addition to untracked files, `f` means force , depends upon `clean.requireForce` config


### Undo last (pushed) commit
`git revert HEAD` This will reverse the effects of an earlier commit (often a faulty one) and record a new commit. The faulty commit will remain in the log list.
