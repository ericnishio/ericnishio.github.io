---
layout: post
title: The Pros and Cons of Building a Website with Jekyll
permalink: /blog/jekyll-pros-and-cons/
---

This website originally started off as a Drupal site, after which I
[rewrote it with AngularJS and Express](http://ericnish.io/blog/how-i-built-this-website/).
Then last year I decided to further simplify it by converting it into a
static website with Jekyll. The motivation was to reduce maintenance
and the cognitive load associated with taking care of an entire jungle
when you just wanted to have a simple website.

I'd like to jot down some of the advantages and disadvantages of
building your website with Jekyll, based on my own experiences.

## Pros

- Jekyll requires no server maintenance.
- No risk of getting hacked (unless somebody guesses your GitHub password).
- Jekyll is fast.
- GitHub is your CMS.
- All your content is versioned in Git.
- Theming is simple.
- No programming involved.
- SEO is baked in.
- GitHub manages 301 redirects and 404s for you.
- Hosting is free on GitHub.
- Custom domains are easy to set up.
- The Jekyll community offers a plethora of plugins for customization.

## Cons

- No server-side scripting (e.g. contact forms).
- Content cannot be dynamically presented (e.g. based on popularity).
- Spinning up a local installation may intimidate non-programmers.
- No post scheduling.
- No image manipulation tool for interactively cropping and resizing images.
