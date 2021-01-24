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

See commits, `space` to see next page, `q` exit
```bash
$ git log
```

Set account's default identity *globally*
```
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
git config --global user.password "your password"
```
Edit account
```
git config --global --edit
```
