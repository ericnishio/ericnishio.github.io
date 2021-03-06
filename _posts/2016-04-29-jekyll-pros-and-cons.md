---
layout: post
title: The Pros and Cons of Building a Website with Jekyll
permalink: /blog/jekyll-pros-and-cons/
---

This website originally started off as a Drupal site, after which I
[rewrote it with AngularJS and Express](/blog/how-i-built-this-website/).
Then in 2015 I decided to further simplify it by converting it into a
static website with Jekyll. The motivation was to reduce maintenance
and the cognitive load associated with taking care of an unnecessarily
complex system when you just wanted to have a simple website.

I'd like to jot down some of the advantages and disadvantages of
building your website with Jekyll, based on my own experiences.

## Pros

- Jekyll requires no server maintenance.
- Low risk of getting hacked (unless somebody acquires your GitHub credentials).
- Jekyll is fast.
- GitHub is your CMS.
- All your content is versioned in Git.
- Theming is simple.
- No programming involved.
- SEO is baked in.
- GitHub manages 301 redirects and 404s for you.
- Hosting is free on GitHub.
- Custom domains are easy to set up.
- Free SSL certificates for custom domains when hosting on GitHub!
- The Jekyll community offers a plethora of plugins for customization.

## Cons

- No server-side scripting (e.g. contact forms).
- Content cannot be dynamically presented (e.g. based on popularity).
- Spinning up a local installation may intimidate non-programmers.
- No post scheduling.
- No image manipulation tool for interactively cropping and resizing images.
