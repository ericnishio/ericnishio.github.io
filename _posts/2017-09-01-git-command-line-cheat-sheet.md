---
layout: post
title: Git Command Line Cheat Sheet
permalink: /blog/git-command-line-cheat-sheet/
---

Here's a list of Git commands I use on a regular basis. I also tend to forget
many of them regularly so it helps to keep them in one place for easy reference.

## Setup

- `git remote add origin git@github.com:username/my-repo.git` Add a remote repository
- `git push -u origin my-branch` Push and set an upstream reference for a branch (first time only)

## Committing

- `git add --patch` Interactively stage changes hunk-by-hunk
- `git commit --amend` Amend the most recent commit
- `git commit --amend --no-edit` Amend the most recent commit without editing the message

## Branching

- `git checkout -b my-branch` Create and check out a new branch
- `git fetch && git checkout my-branch` Check out a remote branch
- `git branch -d my-branch` Delete a branch locally
- `git push origin :my-branch` Delete a branch remotely

## Tags

- `git tag 1.0.0` Create a new tag
- `git push origin --tags` Push all tags to origin
- `git tag -d 1.0.0` Delete a tag locally
- `git push origin :refs/tags/1.0.0` Delete a tag remotely

## Cleaning up

- `git reset --hard` Clear all uncommitted changes
- `git clean -f -d` Delete all untracked files and directories

## Visualization

- `git log --oneline --decorate --graph --all` See a graphical one-line-per-commit representation of all the branches and commits
