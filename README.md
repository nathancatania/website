# Personal Website
[![Netlify Status](https://api.netlify.com/api/v1/badges/1958f9dd-27c6-42b8-b7d9-f11d4dc2f0eb/deploy-status)](https://app.netlify.com/sites/icebreaker-382490/deploys)

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


## Posts
### Content Organization
Posts are created and writtin as markdown `.md` and stored in the `docs/posts/YYYY` directory. All post images go in the relative `assets` folder and are automatically renamed according to `<md_filename>.<timestamp>.<ext>`, eg: `my-post.20240129215322271.webp`

```
.
├── CHANGELOG.md
├── README.md
├── docs
│   ├── assets
│   │   └── avatar.png
│   ├── index.md
│   ├── javascripts
│   │   └── extra.js
│   ├── posts
│   │   ├── 2023
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
    ├── main.html
    └── partials
        ├── header.html
        └── posts-index.html
```

### Front Matter
Each post should start with the following at the top of the markdown documents:
```yaml
---
title: "Insecure Kubernetes for Evaluation Purposes"
icon: material/kubernetes
date: 2023-07-24
description: "This post covers my notes for deploying an app using Kubernetes insecurely for the purposes of evaluating cloud security services."
authors:
  - nathancatania
categories:
  - AWS
  - Kubernetes
  - Security
draft: false
comments: false
---

Post content here
```

`icon` and `comments` are currently not used.

Authors are defined in the `.authors.yml` file.

### Excerpts

These aren't used in the theme, but cause the blog extension to only show the text above the excerpt cutoff for post previews in the default (unmodified) Mkdocs Material theme.

Excerpts are added using the `<!-- more -->` annotation. Anything above this point forms part of the excerpt.

```
The post explores deploying applications on AWS EKS with intentional security flaws to test the effectiveness of cloud security vendors' workload protection solutions.
<!-- more -->

This document will cover the deployment of a containerised public facing web service leveraging Kubernetes; specicially Amazon's managed Kubernetes service: EKS (Elastic Kubernetes Service). As part of this exercise, MongoDB and AWS S3 will also be used and configured insecurely.
```                                                                   |


### Creating a new post
Create a new post via the following:
```
hugo new posts/my-new-post/index.md
```
This will create a folder in `content/posts` called `my-new-folder` and the `index.md` file associated with it. Front matter will automatically be created and inserted into the markdown file (although it will differ from the above slightly).

## Images and Static Content
The `static` folder is used for all static files for the website - images, js, css, and so on.

Files in this folder are served from the site root. For example:
* `static/image.png` can be accessed at `/image.png` or `http://mydomain.com/image.png`
* `static/js/main.js` can be accessed at `/js/main.js`, etc.

Any images or files included in a page bundle (folder for a post that contains the markdown file and all related images and files for that post, eg: `content/posts/my-new-post/...`) are served NOT from the site root, but relative to that folder, eg: `![image](image.png)`.

## Customizing
Don't modify the theme directly (under `themes/hello-friend-ng`). Instead, copy the files you want to change to the appropriate directory in the root of the site, and make your changes to the copy. Hugo will use these files first, before looking in the `themes` folder. This method allows you to use an up-to-date version of the base theme, without having to go through and overwrite your changes again.

For example:
* `/themes/<theme-name>/layouts/...` -> `/layouts/...` (anything HTML or relating to structure)
* `/themes/<theme-name>/static/fonts/...` -> `/static/fonts/...` (fonts, or anything static to be served)
* `/themes/<theme-name>/assets/scss` -> `/assets/scss/...` (scss, so essentially any style changes you make)

You may need to manually create the `assets` folder in the site root.

## Deployment
### Initial Deployment
The Hugo team have posted a great guide to initial deployment with Netlify [here](https://gohugo.io/hosting-and-deployment/hosting-on-netlify/).

### Updates
Netlify will build and redeploy the site every time changes are pushed to the git repo; no additional taks required (CD).

## TODO
* Customize archetype to use correct front matter
* Re-add comments (?)
* Favicons