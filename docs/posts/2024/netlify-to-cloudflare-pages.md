---
title: "Migrating my website from Netlify to Cloudflare Pages"
icon: simple/cloudflarepages
date: 2024-04-02
description: "I recently moved my blog (this website) from Netlify to Cloudflare pages. This post covers the process I went through."
authors:
  - nathancatania
categories:
  - Web
  - Reflection
draft: false
comments: false
---

In February this year (2024), I went through the process of migrating this website from Netlify to Cloudflare Pages. I thought this would be a straightforward process - my website is a static site comprised of simple HTML after all - but alas, as most projects go, something that should have been a 30 minute job turned into a 3 days of work.

Why move a personal project from Netlify? Two reasons:

1. Analytics: I was running no analytics for my site. Why? The webiste is a "*when I feel like it*" side-project, and I didn't want to go down the path of client-side analytics like Google Analytics for privacy reasons. Netlify charges US$9/month for analytics derived from their CDN, and I was curious as to what content on my site people were looking at, but not US$9/month curious.
2. [This worrying post](https://web.archive.org/web/20240321064532/https://www.reddit.com/r/webdev/comments/1b14bty/netlify_just_sent_me_a_104k_bill_for_a_simple/) where Netlify sent a free tier user a US$104K bill. [Related HackerNews discussion](https://web.archive.org/web/20240302032136/https://news.ycombinator.com/item?id=39520776).

Point #1 was my primary reason, but point #2 was the catalyst for me to actually go and do something about it. I selected Cloudflare Pages as, like Netlify and GitHub pages, there is a free tier that is perfect for hobby use, but unlike Netlify, Cloudflare includes basic website analytics for free.

## The old website

[My old website](https://github.com/nathancatania/website-2020) used Hugo as a static site generator with a customized version of the [Hello Friend NG theme by rhazdon](https://github.com/rhazdon/hugo-theme-hello-friend-ng).

![The old website](https://github.com/nathancatania/website-2020/raw/master/demo/images/banner.png)

Honestly, this combination was pretty good! The theme looked sharp, Hugo was relatively easy to use, and the static site meant that content loaded quickly. Not bad for a total monthly cost of $0!



