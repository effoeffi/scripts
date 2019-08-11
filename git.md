# Git

Clone a repository into a new directory
```bash
$ git clone https://github.com/effoeffi/scripts.git
```

Switch branches and create a new branch (with `-b`)
```bash
$ git checkout -b new_branch
```

Remove all your local git branches but keep master
```bash
$ git branch | grep -v "master" | xargs git branch -D
```
