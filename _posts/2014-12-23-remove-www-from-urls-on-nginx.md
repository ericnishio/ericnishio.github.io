---
layout: post
title: Remove WWW from URLs in nginx
permalink: /blog/remove-www-from-urls-on-nginx/
---

Simply create two server configurations where the first server name redirects
to the second one. No regular expressions needed.

{%highlight nginx %}
server {
  server_name www.example.com;
  return 301 $scheme://example.com$request_uri;
}

server {
  server_name example.com;
  # the rest of your configuration
}
{% endhighlight %}
