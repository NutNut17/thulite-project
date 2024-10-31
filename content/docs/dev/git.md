---
title: "Git"
description: ""
summary: ""
date: 2024-10-18T20:27:34+08:00
lastmod: 2024-10-18T20:27:34+08:00
weight: 301
draft: false
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

### Source Control

Git is a tool to track changes in a working directory(repository), a perfect tool to control the version of developement in local enviroment. While Github is an online repository platform allowing developers to save, share and deploy codes online.

### Workflow and Concept

Three trees maintained by git

1. Working Directory    --> add to Index
2. Index: staging area  --> commit to HEAD
3. HEAD: A pointer, points to last commit

### Getting Started

```bash
git init
git add .
git commit -m "Initial Commit"
```

### GitHub

To use GitHub, create a repository on Github and copy the repository link `https://github.com/username/repository.git`.

```bash
git remote add origin https://github.com/username/repository.git
git push -u origin master
```

### Checkout

Switches working directory to the target branch. Example below switch to main

```bash
# Move to branch
git checkout main
# Create and switch to new branch
git checkout -b <branch>
# Delete unused branch
git push origin <branch>
```

origin: default name of remote repository when cloned
main: mainline branch of project
master: legacy name of main

### Update and Merge

```bash
# Fetch and merge remote changes
git pull
```

```bash
# Merge to active branch
git merge <branch>
```

Git will show the conflict, edit the files to resolve conflict

```bash
# After resolving conflict
git add <filename>
# Preview before merging
git diff <source_branch> <target_branch>
```

### Tagging and Logging

Tags for software release. The code is the first 10 characters of commit id. View log for commit id details.

```bash
git tag 1.0.0 1b2e1d63ff
```

```bash
git log
git log --author=bob
git log --pretty=oneline
git log --graph --oneline --decorate --all
git log --name-status
git log --help
```

### Replace local changes

```bash
# Replace these files into previos update
git checkout -- <filename>
```

```bash
# Forget local and use newest from server
git fetch origin
git reset --hard origin/master
```

### Hints

```bash
# built-in git GUI
gitk
# use colorful git output
git config color.ui true
# show log on just one line per commit
git config format.pretty oneline
# use interactive adding
git add -i
```

Reference: [git-guide](https://rogerdudler.github.io/git-guide/)
