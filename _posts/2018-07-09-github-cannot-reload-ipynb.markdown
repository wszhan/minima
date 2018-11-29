---
layout: post
title:  "Can't Load Jupyter Notebook on GitHub"
date:   2018-07-09 17:00:00 +0800
categories: 
---

Very often while trying to load a Jupyter Notebook file in GitHub repo, you will see this:

```
Sorry, something went wrong. Reload?
```

To solve this, a workaround would be using a site called `https://nbviewer.jupyter.org/`.

Steps:

- Open the website: https://nbviewer.jupyter.org/

- Go to the page of your jupyter notebook page, where the url is like 
```
https://github.com/wszhan/tv-script-generation_the-simpsons/blob/master/dlnd_tv_script_generation.ipynb
```

- Combine the two urls into something like
```
https://nbviewer.jupyter.org/github/wszhan/tv-script-generation_the-simpsons/blob/master/dlnd_tv_script_generation.ipynb
```

And you will see notebook loaded.

References:

- ["Sorry, something went wrong. Reload?" when viewing *.ipynb #11](https://github.com/iurisegtovich/PyTherm-applied-thermodynamics/issues/11#issuecomment-323842311)