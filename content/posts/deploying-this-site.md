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

So, it's the week of Thanksgiving 2019. I have the week off, and while my focus
is and has been on spending my time off with my wife and our 3 year old son,
they are both asleep right now and I have been able to steal 10 minutes here, 15
minutes there.

I've found that being as disorganized as I can be, writing things down and
making lists help me keep track of my plan-of-attack and focus my efforts. I
used to think I could keep everything in my head, but I tell you - that is a
young person's game. Smarter, not harder. Write it down. 

My list started off as follows:

- update personal computer
- install/update go
- create/init Hugo blog project
- create index page
- create 404 page/coming soon page
    - svg animation
- deploy via netlify and fw from bwynn.io

First: I pulled out my computer, my personal MacBookPro. It's a 2013, and I have
been using a 2019 MBP (no, not the 16") for the last few months, and the
keyboard is a switch! Heyo! 

Updated software, `brew cleanup`, and `brew install golang`, and I had the first
two items ticked off my list. 

Going through the Hugo docs and getting started was really easy, I followed it
to a 'T', through deployment via Netlify. Probably took me 30 minutes to get
everything set up. Now that said, if you are interested in using Hugo and are in
the process of learning Go, I would strongly recommend a visit over to the [Go
Docs](https://golang.org/doc/code.html), where there is a deep-dive on setting
up your local Go environment - which is crucial to that `Probably took me 30
minutes...` part a few sentences ago. Thoroughly go through the docs to ensure
you get your environment and `env` variables all properly set up, or else add
' * x' to the amount of time estimated to get set up - 'x' being your speed.

I tend to go pretty slow, and skip over crucial sentences in documentation, and
execute things before I'm supposed to; and can create a mess - I don't want to
venture how long it took me to get my go environment set up properly the first
time, it wasn't until I had figured out how to resolve my mangled `PATH` env
variable and its relation to the go binary. Lets call it a week and then voila,
if it takes you less time than that, genius! If it took you a week or longer,
there's still hope, as someone has chosen to continue sending me paychecks.

The hope and goal for this blog is to provide a positive reinforcement chamber
to visit to help both you and me remember that if we don't give up, we'll
eventually get there. Persistence is one of the key attributes that help me grow
as a developer. We WILL find the answer. An answer. Any answer. Make it work
first, then make it nice.

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
initially available.

### Persistent CORS issues
So I finally get a rough template and draft static site going in my Hugo
dev environment, and decide that I'll switch my domain forwarder to point to my
Netlify site. Needs 48 hours to verify the certs. Okay, I can play the waiting
game - pack up the family, drive to my wife's Mom's house 4 hours away, do
Thanksgiving. Last night, after dinner, I pull up my site to see if the certs
have validated. They have! WooHoo! Maybe all the status error issues I was
seeing will go away. All do - except for the failed hashed-stylesheet that was
generated via hugo as part of the vendor stylesheets that come with the
Hugo-Coder theme. 

I still see an `Access-Control-Allow-Origin` error. A quick search of `netlify
CORS Access-Control-Allow-Origin` gave me a quick pointer to this [handy
doc](https://docs.netlify.com/configure-builds/file-based-configuration/#sample-file),
which would have been nice to see more prominently in Netlify's docs.

Adding the following config file to my project directory with the defined
headers set to accept any origin like so: 

**netlify.toml**
```yaml
[headers]
    for = "/*"
    [headers.values]
        Access-Control-Allow-Origin = "*"
```

I'll plan to update this later, but for all
intents and purposes, my goal has been to get the site loading without any
errors.

### Wrapping Up
As I sit here on the Saturday night after Thanksgiving, I checked off all of the
items on my list with the exception of the svg 404 animation. I have an idea as
to how I'd like to go about this, but I want to be able to spend some concerted
time sketching out the animation and then digitizing it. Maybe I'll save that
for the next break, coming up in a few weeks. Instead, we have this post -
switching my deployment pipeline to Netlify from Heroku, along with a fresh new
website, which is really nicely put together from a developer's perspective. I
have been pretty impressed with my experience thus-far!

Best part: I was able to get all of this done working around the various
bookends of the day - I didn't have to cut into quality time (okay maybe 5
minutes!) with my family to get this done by the end of my break.

Lessons learned - take some screen shots to add into my posts. I do it at work -
what gives 🤷‍♂️?!

This would also be a good time to mention the developer who built this awesome
Hugo theme, [Luiz de Prá](https://github.com/luizdepra/hugo-coder/) and has some
great documentation around this theme - muito obrigado!

Thanks everyone for taking the time to stop by and read my post, I hope that my fumbling
around can help shine a light in a direction that works for you.
