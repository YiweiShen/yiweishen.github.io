title: Simple Notes for Git
date: 2020-11-06 15:45:50
tags:
---

These notes are for easy reference since I am new to Git.

You can clone the particular branch in the repo.
```bash
git clone -b branch-name
```

After you have done the git clone your repo to the local device, go inside the repo folder via terminal. You can check git status or check which branch you are in.
```bash
git status
git branch -a
```

If you want to double check if origin is correct.
```bash
git remote -v
```

You can fetch the branches along with their respective commits, but not the actual files.
```bash
git fetch
```

If you need to synchronize your branch list, for example, a branch is delete on github but not on your local machine.
```bash
git fetch -p
```

You can pull actual files with info such as the branches with the respective commits.
```bash
git pull
```

You can create and checkout the new branch at the same time.
```bash
git checkout -b new-branch
```

After working on your file you can add the particular file to this branch.
```bash
git add filename
```

Or add all file in the current folder to this branch.
```bash
git add .
```

Then you can make a commit locally, remember always to add some comments for your commit.
```bash
git commit -m "Fixed some typos"
```

If you are using GPG to sign your commit, add -S in the end.
```bash
git commit -m "Fixed some typos" -S
```

Normally, you can now push your new-branch together with the new commit to Github. Later you can go to pull request on Github.
```bash
git push origin new-branch
```

Or perhaps you want to merge the new-branch locally with your master branch. First, go back to master branch then merge.
```bash
git checkout master
git merge new-branch
```

If you have sucessfully merged the branches, you can choose to delete your previous new-branch locally. Be careful here.

The -d option stands for --delete, which would delete the local branch, only if you have already pushed and merged it with your remote branches.

The -D option stands for --delete --force, so by the name, you can guess it will delete the local branch no matter if you have pushed/merged or not.

So, please be extra careful. I suggest you use -d unless you are totally sure and have double checked the git status.

```bash
git branch -d new-branch
git branch -D new-branch
```

If you previously have pushed the new-branch to Github and now you want to delete it remotely, yes, you can.
```bash
git push origin --delete new-branch
```



When in doubt, please read documentations.
https://www.git-scm.com/doc
