---
layout: post
title: Git Command Line Cheat Sheet
permalink: /blog/git-command-line-cheat-sheet/
---

Here's a list of Git commands I use on a regular basis. I also tend to forget
many of them regularly so it helps to keep them in one place for easy reference.

## Setup

- `git remote add origin git@github.com:username/my-repo.git` adds a remote repository
- `git push -u origin my-branch` pushes and sets up an upstream reference for a branch (first time only)

## Committing

- `git add --patch` interactively stages changes hunk-by-hunk
- `git commit --amend` amends the most recent commit
- `git commit --amend --no-edit` amends the most recent commit without editing the message

## Branching

- `git checkout -b my-branch` creates and checks out a new branch
- `git fetch && git checkout my-branch` checks out a remote branch
- `git branch -d my-branch` deletes a branch locally
- `git push origin :my-branch` deletes a branch remotely

## Tags

- `git tag 1.0.0` creates a new tag
- `git push origin --tags` pushes all tags to origin
- `git tag -d 1.0.0` deletes a tag locally
- `git push origin :refs/tags/1.0.0` deletes a tag remotely

## Cleaning up

- `git reset --hard` clears all uncommitted changes
- `git clean -f -d` deletes all untracked files and directories

## Visualization

- `git log --oneline --decorate --graph --all` shows a graphical one-line-per-commit representation of all branches and commits
