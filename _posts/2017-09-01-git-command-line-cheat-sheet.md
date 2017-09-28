---
layout: post
title: Git Command Line Cheat Sheet
permalink: /blog/git-command-line-cheat-sheet/
---

Here's a list of Git commands I use on a regular basis. I also tend to forget
many of them regularly so it helps to keep them in one place for easy reference.

If you have [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh){:target="_blank"}
installed it comes with an assortment of
[Git aliases](https://github.com/robbyrussell/oh-my-zsh/blob/456341fd69c3e514e401f1c3c1726b77d733c86b/plugins/git/git.plugin.zsh#L41){:target="_blank"} that covers many of the commands listed below.

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
- `git branch -r` lists remote branches

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
- `git log -p -S"console.log"` shows the commits that contain the searched text (use `-i` to ignore case and `--no-merges` to exclude merges)
- `git log -p README.md` shows the commits and changes applied to a specific file
- `git log -p --after="2 weeks ago" README.md` shows the commits and changes applied to a file after a date

## Find a breaking commit with bisect

1. `git bisect start` begins a bisect session
2. `git bisect bad` marks the current commit as broken
3. `git bisect good` marks the current commit as healthy, and checks out the next testable commit
4. Test the commit and run `git bisect bad` or `git bisect good`
5. Keep testing and marking until you are left with the commit that first introduced the bug
6. `git bisect reset` resets to the original state
