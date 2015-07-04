---
layout: post
title: Build tags page and markdown support in Git Pages
categories: [Records]
tags: [jekyll]
published: True

---

## Tags

By default, the Jekyll in Git Pages disabled plugins so that it is difficult to adopt additional features such as tags. I found a [workaround](https://blog.brandonparsons.me/2015-using-tags-in-a-jekyll-blog-on-github-pages/) which is easy to build and looks nice.


## Markdown in Jeklly

There are a few markdown interpreter in Jeklly but not all of them have full support for GFM (Github Favored Markdown). I used *kramdown* but did not manage to display a code block. I switched to *redcarpet* and manage to make the posts displayed in GFM. A good guide can be found [here](http://milanaryal.com/2015/writing-on-github-pages-and-jekyll-using-markdown/).

