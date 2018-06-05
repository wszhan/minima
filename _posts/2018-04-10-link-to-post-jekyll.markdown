---
layout: post
title:  "Create a Link to Another Page in a Jekyll Post"
date:   2018-04-10 17:35:33 +0800
categories: 
---

#### Link to Another Post

It is actually a **Markdown** problem. And Jekyll has provided the code in its [documentation](https://jekyllrb.com/docs/templates/#linking-to-posts). However, it still took me a few tries to understand.

The example code in the documentation is [here](https://jekyllrb.com/docs/templates/#linking-to-posts).

Explanation of the example code:
- ```[Name of Link]``` is just a name. It can be anything.
- Do not modify ```site.baseurl```. Your ```baseurl``` will replace the ```site.baseurl``` here in the link.
- Do not modify ```post_url``` neither. This is just a tag.
- ```2010-07-21-name-of-post``` is the name of the post you want the link points to.

#### Link to Another Page in General

If the intended destination of the link is not a post but another page, the `post_url` must be replaced by `link` and it must be followed by the path plus page name, such as `news/docs.html`.

References:

- [jekyll markdown internal links
](https://stackoverflow.com/questions/4629675/jekyll-markdown-internal-links?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa)