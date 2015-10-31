---
layout: post
title: How to Delete Git Tags
permalink: /blog/how-to-delete-git-tags/
---

In this example we will be deleting a tag labeled 1.0.0.

Locally:

```
$ git tag -d 1.0.0
```

Remotely:

```
$ git push origin :refs/tags/1.0.0
```
