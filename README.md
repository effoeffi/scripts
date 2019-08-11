# scripts

#### Git
Remove all your local git branches but keep master
```bash
$ git branch | grep -v "master" | xargs git branch -D
```

Switch branches and create a new branch (with `-b`)
```bash
$ git checkout -b new_branch
```
