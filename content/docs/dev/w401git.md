---
title: "Git"
description: ""
summary: ""
date: 2024-10-18T20:27:34+08:00
lastmod: 2024-10-18T20:27:34+08:00
weight: 401
draft: false
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

### Source Control

{{< inline-svg src="svgs/logos/git-icon.svg" width="100px" height="79px" class="svg-inline-custom" >}}

Git is a tool to track changes in a working directory(repository), a perfect tool to control the version of developement in local enviroment. While GitHub is an online repository platform allowing developers to save, share and deploy codes online.

### Online Git Platform

<div class="container-fluid" style="margin: 3rem">
    <div class="row">
        <div class=" col-12 col-sm-4 flex-fill">
          {{< inline-svg src="svgs/logos/github-icon.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
        <div class=" col-12 col-sm-4 flex-fill">
          {{< inline-svg src="svgs/logos/gitlab.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
        <div class=" col-12 col-sm-4 flex-fill">
          {{< inline-svg src="svgs/logos/bitbucket.svg" width="100px" height="79px" class="svg-inline-custom" >}}
        </div>
    </div>
  <div class="row">
      <div class="col-12 col-sm-4 flex-fill">
          <h4>GitHub</h4>
      </div>
      <div class="col-12 col-sm-4 flex-fill">
          <h4>GitLab</h4>
      </div>
      <div class="col-12 col-sm-4 flex-fill">  
          <h4>BitBucket</h4>
      </div>
  </div>
</div>

| Feature | GitHub | GitLab | Bitbucket |
| - | - | - | - |
| Free Repos | Unlimited | Unlimited | Limited to 5 users |
| CI/CD | GitHub Actions | Built-in | Pipelines |
| Self-Hosting | No | Yes | Yes |
| Integration | Widely supported | GitLab-exclusive | Atlassian tools |
| Best For | Open-source projects, team collaboration | Enterprises and teams focused on DevOps workflows | Teams using Atlassian tools |

### Workflow and Concept

Three trees maintained by git

1. Working Directory: to be added to Index
2. Index(staging area): to be commited to HEAD
3. HEAD: a current pointer in branch

`origin`: default name of remote repository when cloned, `main`: mainline branch of project, `master`: legacy name of main. To make different code from main branch, ALWAYS create a new branch and merge after completion. Checkout switches working directory to the target branch.

### Getting Started

```bash
git init    # Create git repository
git add .   # Stash
git commit -m "Initial Commit Message"
```

### Branching and Merging

```bash
# Create a branch
git branch <branch_name>
# Move to a branch
git checkout <branch_name>
# Create and switch to new branch
git checkout -b <branch_name>
# Delete unused branch
git branch -d <branch_name>

# Merge HEAD to a branch
git merge <branch_name>
```

Rebase moves entire branch in HEAD to begin on the tip of a branch. It is better for a cleaner linear history. But are not suitable for beginer and collaboration.

```bash
git rebase <branch_name>
```

Detach is a way to move a HEAD to previous commit.

```bash
git checkout <commit_id>
# Move to the parent of branch_name
git checkout <branch_name>^
# Move to the second parent of branch_name
git checkout <branch_name>^2
# Move to the n-th parent of branch name
git checkout <branch_name>~n

# Force the first branch to the parent of second branch. Unable to work on current branch. The moved branch will lost it's commit
git branch -f <branch_name> <branch_name>^
```

Reset reverse the changes by moving a branch to its parent. But it only works on local. While revert reverse the change, it will add a new commit so that the branch is now the same as its previous parent. This is recommended for collaborative work.

```bash
git reset HEAD~1
git revert HEAD
```

If there was unresolvable merge, git will show the conflict. Edit the files to resolve conflict.

```bash
# After resolving conflict
git add <filename>
# Preview before merging
git diff <source_branch> <target_branch>

# Cherry-pick picks the commits to be added into HEAD
git cherry-pick <commit1> <commit2>
# Interactive rebase: pick the arrangement of a branch into a new branch
git rebase -i HEAD~4
git rebase <destination_branch> <source_branch>
```

### Pushing and Pulling

```bash
# Fetch and merge remote changes to stay synced
git pull
# Remove references to branches that no longer exist on the remote
git fetch --prune
git pull --rebase

# Update a remote branch
git push origin <branch_name>
# Update all remote branch
git push --all origin
# Delete a remote branch
git push origin --delete <branch_name>
```

### Tagging

Tags for software release. The code is the first 10 characters of commit id. View log for commit id details.

```bash
git tag 1.0.0 1b2e1d63ff
```

### Logging

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
Visual Tutorial: [Learning Git](https://learngitbranching.js.org/?locale=en_US&source=post_page-----c5dc0639dd9--------------------------------)

### GitHub

{{< inline-svg src="svgs/logos/github-icon.svg" width="100px" height="79px" class="svg-inline-custom" >}}

To use GitHub, create a repository on Github and copy the repository link `https://github.com/username/repository.git`.

```bash
git remote add origin https://github.com/username/repository.git
git push -u origin master
```

GitHub repository have its own branch based on GitHub users. On each branch of user, the repository have its own branch. After a user fork a GitHub repository, that user can open a `Pull Request` to merge the fork back to the original branch and is to be reviewed by the original author.

### Git on VS Code

VS Vode comes with a pre-built git UI system. It will detect a git repository on the opened folder and display on `Source Control`. Here are some common functions:

1. Click `commit` and insert the message to update graph tree. Conflict resolver will appear automatically if needed.
2. Create and checkout branch on `More Action...`
3. Press `Fetch From All Remotes` and click `SYNC` to update to latest remote repository

Alternately, Git Graph extension is also quite intuitive and easy to manage git visually.
