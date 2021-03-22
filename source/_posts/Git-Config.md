---
title: Git_Config
date: 2021-03-22 17:39:15
tags: Web Development
---

# Git

## How to configure a computer with git
* `git config --global user.name "your-name"`
* `git config --global user.email "your-email"`


To check if Git is already configured you can type:
`git config --list`


## How to merge code
1.**Create a branch**
* `git branch [branch-name]`

2.**Switch to working branch**
* `git checkout [branch-name]`

3.**Do work**
* `git add .`
* `git commit -m 'my changes'`

4.**Combine your work with `main` branch**. The `main` branch might have chagned, so pull it first
* `git checkout main`
* `git pull`

At this point you want to make sure that no conflicts happened. Therefore run the following commands.
* `git checkout [branch-name]`
* `git merge main`


5.**Send your work to Github**. Pushing your branch to your repo and then open up a PR, Pull Request.
* `git push --set-upstream origin [branch-name]`

6.**Open a PR**. Next, you want to open up a PR. You do that by navigating to the forked repo on GitHub. You will see an indication on GitHub where it asks whether you want to create a new PR, you click that and you are taken to an interface where you can change commit message title, give it a more suitable description. 

7.**Clean up**. It is good practise to clean up the code after you successfully merge a PR.
* `git branch -d [branch-name]`

