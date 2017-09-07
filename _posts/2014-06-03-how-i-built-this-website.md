---
layout: post
title: How I Built This Website
permalink: /blog/how-i-built-this-website/
---

> I recently rebuilt this website with Jekyll so the technology stack described
> in this post no longer applies to the current version of the site (as of
> October 2015). The reason why I switched to Jekyll is that I didn't really
> need all the back-end services I had originally set up since I could simply
> serve the content as static files on GitHub. The website itself is very
> minimal so I decided to take an equally minimal approach and use
> [Jekyll](https://jekyllrb.com) and [GitHub Pages](https://pages.github.com).

## Key technologies used

* Node
* Express
* AngularJS
* MongoDB with Mongoose
* nginx
* Mandrill
* Prerender
* Disqus

## Development process

This website originally started off as an experiment—a simple prototype I was
writing with AngularJS because I wanted to get better acquainted with the
framework. But as I kept on adding more parts to it, it eventually evolved
into ericnishio.com v2.0, with a fitting .io TLD.

I had originally built the website with Drupal, but since Drupal sites tend to
be slow unless you have effective caching mechanisms in place, I thought
switching platforms would be a nice change, and I'd get to learn something
new.

So I stuck with the Angular prototype I had written, and took Express to
construct a RESTful API for communicating with the client-side app.

It took me a bit over a month (part-time) to complete the application base. So
in mid-May,  2014, I decided to set up a fresh VPS on [DigitalOcean](https://www.digitalocean.com/?refcode=fbbb0e38c242) and deploy
the site. I wasn't expecting such a smooth first-time deployment experience,
but things turned out surprisingly well. Running the API server on top of a
minimal nginx configuration worked like a charm.

I didn't have an admin account for writing content with so I also wrote a Node
command-line tool for creating, listing, and deleting user accounts. For
token-based authentication I decided to use JSON Web Token. To expose the
asynchronously loaded content to search engine crawlers, I deployed a
Node-powered [Prerender](http://prerender.io) server for rendering static web
pages in the background.

What I particularly like about Node is the fact that I can now do everything
in JavaScript—even the server-side components. And it feels really good.

I carved out the cosmetic appearance of the website with Twitter Bootstrap. I
wanted to create a minimal look so my design work chiefly consisted of
choosing a clean font and giving the elements ample whitespace around them. I
also decided not to support image attachments so the syntax-highlighted code
blocks are the only visual sugar added to the otherwise plain text blog posts.

If I were to do the same project over again, I would do some things
differently. Although I'm overall very satisfied with what I was able to
accomplish, the one thing I would do differently is use
[Sails](http://sailsjs.org) for building the API. By utilizing the solid
foundation that Sails provides, I would have written less code and focused on
building functionality and spent less time on scaffolding the project. But
using Express instead of Sails (which is built on top of Express) gave me a
broader understanding of the underlying nuts and bolts that have been
abstracted away in Sails. So ultimately from a learner's point of view the
outcome was pure victory.
