---
title: Hosting Hugo Website In Cloudflare
description: 
published: true
date: 2026-03-31T17:13:03.308Z
tags: 
editor: markdown
dateCreated: 2026-03-29T16:18:57.249Z
---

This guide shows how to setup a hugo site with  cloudflare. Prequisites are having a github repository with your hugo project ready to go.

# Hugo
* An open source free to use static site genorator. It includes templates to customized the site to your liking.
* Uses markdown files to generate site content
* Easily hosted by cloudflare, updates are automatically applied when repo is updated
* [Hugo Documentation](https://gohugo.io/)

# Setup Steps

1. Navigate to compute -> Workers & Pages
![create-page.png](https://cdn.todoprogramming.org/create-page.png)
2. Click create application
3. Click  [Getting Started](https://dash.cloudflare.com/a151a0cb99ae3e03d38e3590438bf20d/workers-and-pages/create/pages) at the bottom
![screenshot_from_2026-03-29_11-36-56.png](https://cdn.todoprogramming.org/screenshot_from_2026-03-29_11-36-56.png)

4. import existing  repository
![getting-started-with-pages-1.png](https://cdn.todoprogramming.org/getting-started-with-pages-1.png)

![getting-started-with-pages-2.png](https://cdn.todoprogramming.org/create-page.png/getting-started-with-pages-2.png)

5. configure for hugo
![getting-started-with-pages-3.png](https://cdn.todoprogramming.org/getting-started-with-pages-3.png)

6. Select Domain
![getting-started-with-pages-select-domain.png](https://cdn.todoprogramming.org/getting-started-with-pages-select-domain.png)