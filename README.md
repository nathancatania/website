# Personal Website

My personal website ([nathancatania.com](https://nathancatania.com)) created with [Mkdocs Material](https://github.com/squidfunk/mkdocs-material) and served with [Cloudflare Pages](https://pages.cloudflare.com/).

## Setup
1. Clone the repository:
```
git clone https://github.com/nathancatania/website.git
```

2. Create and activate new virtual environment:
```
python3 -m venv venv
source venv/bin/activate
```

3. Install required software for Social Cards extension:
```
brew install cairo libffi
export LDFLAGS="-L/opt/homebrew/opt/libffi/lib"
export CPPFLAGS="-I/opt/homebrew/opt/libffi/include"
export PKG_CONFIG_PATH="/opt/homebrew/opt/libffi/lib/pkgconfig"
```

4. Install Mkdocs Material and Plugins:
```
pip install mkdocs-material
pip install cairosvg
pip install 'mkdocs-material[imaging]'
pip install mkdocs-git-revision-date-localized-plugin
pip install mkdocs-git-committers-plugin-2
```

## Run Locally
Use the `mkdocs serve` command to build the documentation and run it on a local webserver @ `http://127.0.0.1:8000/`

```
mkdocs serve

INFO    -  Building documentation...
INFO    -  Cleaning site directory
INFO    -  Documentation built in 0.29 seconds
INFO    -  [15:36:39] Watching paths for changes: 'docs', 'mkdocs.yml'
INFO    -  [15:36:39] Serving on http://127.0.0.1:8000/
```

You can also specify a port manually:
```
mkdocs serve -a 127.0.0.1:8888
```

## Deploying
Push changes to the main branch.
Cloudflare Pages will automatically rebuild the site and deploy it.

If dependencies change, re-run:
```
pip freeze > requirements.txt
```

If deploying from scratch for the first time, follow [this CF documentation for deploying a Mkdocs site](https://developers.cloudflare.com/pages/framework-guides/deploy-an-mkdocs-site/).


## Posts
### Content Organization
Posts are created and writtin as markdown `.md` and stored in the `docs/posts/YYYY` directory. All post images go in the relative `assets` folder and are automatically renamed according to `<md_filename>.<timestamp>.<ext>`, eg: `my-post.20240129215322271.webp`.


```
.
├── CHANGELOG.md
├── README.md
├── docs
│   ├── assets
│   │   ├── avatar.png
│   │   └── favicon.png
│   ├── index.md
│   ├── javascripts
│   │   └── extra.js
│   ├── posts
│   │   ├── 2024
│   │   │   ├── assets
│   │   │   │   ├── another-post.timestamp1.png
│   │   │   │   ├── another-post.timestamp2.png
│   │   │   │   ├── safe-post-title.timestamp1.png
│   │   │   │   ├── safe-post-title.timestamp2.png
│   │   │   │   └── safe-post-title.timestamp3.png
│   │   │   ├── safe-post-title.md
│   │   │   └── another-post.md
│   └── stylesheets
│       └── extra.css
├── mkdocs.yml
└── overrides
    ├── blog.html
    ├── landing.html
    ├── main.html
    └── partials
        ├── header.html
        └── posts-index.html
```

Use the Obsidian Attachment Management Community Plugin with the following settings to automatically rename and move images for posts into their appropriate directory. If not automatically invoked, you can run it using the "Attachment Management: Rearrange Linked Attachments" command.

  - Root path: Copy Obsidian
  - Attachment path: `${notepath}/assets`
  - Attachment format: `${notename}.${date}`
  - Date format: `YYYYMMDDHHmmssSSS`
  - Automatic rename: `true`
  - Excluded paths: `.obsidian/;site/;venv/;docs/assets/;.git;`
  - Exclude subpaths: `true`

### Front Matter
Each post should start with the following at the top of the markdown documents:
```yaml
---
title: "This is a blog post title"
date: 2023-07-24
description: "This is a description of the post that is used for SEO."
authors:
  - nathancatania
categories:
  - Category1
  - Category2
  - Category3
draft: false
comments: false
---

Post content here
```

`comments` is not currently used.

Authors are defined in the `.authors.yml` file.

### Excerpts

These aren't used in the theme, but cause the blog extension to only show the text above the excerpt cutoff for post previews in the default (unmodified) Mkdocs Material theme.

Excerpts are added using the `<!-- more -->` annotation. Anything above this point forms part of the excerpt.

```
The post explores deploying applications on AWS EKS with intentional security flaws to test the effectiveness of cloud security vendors' workload protection solutions.
<!-- more -->

This document will cover the deployment of a containerised public facing web service leveraging Kubernetes; specicially Amazon's managed Kubernetes service: EKS (Elastic Kubernetes Service). As part of this exercise, MongoDB and AWS S3 will also be used and configured insecurely.
```