+++ 
draft = false
date = 2019-11-29T20:51:13-08:00
title = "Deploying this site"
description = "process for migrating everything over to this site"
slug = "deploying-new-site" 
tags = []
categories = []
externalLink = ""
series = []
+++

## Background

**I haven't changed my site in over 3 years.**

### Why the need for the change?

At the time that I last worked on my site, it was to make sure that I had
everything properly hosted while I was interviewing for my current job. I
wrote bwynn.io in jQuery and my goals and objectives were different than my
needs are now.

I saw a convergence of my various responsibilities in life open up for a chance
to delve into [Hugo](https://gohugo.io). It seemed like the right platform to
host my site, as my goals are to work on my writing/blogging, and to do some
light [golang](https://golang.io) in my spare-time. I get to use go at work, but
I spend a vast majority of my time in JavaScript-land, and want to have a reason
to stay somewhat on top of things as long as I'm not directly working on a
project in go at work.

### Issues switching DNS proxies/redirects.
My domain is hosted through [google domains](https://domains.google.com) - I had
briefly considered throwing the static site up on a linode-node, but opted to
use [netlify](https://netlify.com) to handle the deployment and CI. While I had
previously deployed my site via Herkou, which has a similar DNS forwarding tools
as Netlify. In both cases, I have the site proxied through bwynn.io and then
pointing/forwarding along to the Netlify address.

Configuring my site deployment through Netlify has for the most-part, been a
breeze.

### CORS issues with Netlify and Hugo-Coder theme
My only gripe using Netlify as my deployment pipeline thus far is that
configuring some initial headers took a bit more digging to properly resolve the
CORS issue I was seeing. Some of the `netlify.toml` config details weren't
initially available, but hey - I feel as though I am fairly resourceful and was
able to determine that my netlify config file required setting the following:

**config.toml**
```yaml
[headers]
    for = "/*"
    [headers.values]
        Access-Control-Allow-Origin = "*"
```

