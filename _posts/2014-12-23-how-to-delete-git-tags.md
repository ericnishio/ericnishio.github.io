---
layout: post
title: How to Delete Git Tags
permalink: /blog/how-to-delete-git-tags/
tags:
  - hidden
---

In this example we will be deleting a tag labeled 1.0.0.

Locally:

{% highlight bash %}
$ git tag -d 1.0.0
{% endhighlight %}

Remotely:

{% highlight bash %}
$ git push origin :refs/tags/1.0.0
{% endhighlight %}
