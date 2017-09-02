---
layout: post
title: Git Command Line Cheat Sheet
permalink: /blog/git-command-line-cheat-sheet/
---

Here's a list of Git commands I use on a regular basis. I also tend to forget
many of them regularly so it helps to keep them in one place for easy reference.

## Setup

- Add a remote repository `git remote add origin git@github.com:username/my-repo.git`
- Push and set an upstream reference for a branch (first time only) `git push -u origin my-branch`

## Committing

- Interactively stage changes hunk-by-hunk `git add --patch`
- Amend the most recent commit `git commit --amend`
- Amend the most recent commit without editing the message `git commit --amend --no-edit`

## Branching

- Create and check out a new branch `git checkout -b my-branch`
- Check out a remote branch `git fetch && git checkout my-branch`
- Delete a branch locally `git branch -d my-branch`
- Delete a branch remotely `git push origin :my-branch`

## Tags

- Create a new tag `git tag 1.0.0`
- Push all tags to origin `git push origin --tags`
- Delete a tag locally `git tag -d 1.0.0`
- Delete a tag remotely `git push origin :refs/tags/1.0.0`

## Cleaning up

- Clear all uncommitted changes `git reset --hard`
- Delete all untracked files and directories `git clean -f -d`

## Visualization

- See a graphical one-line-per-commit representation of all the branches and commits `git log --oneline --decorate --graph --all`
