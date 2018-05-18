---
layout: post
title:  "Extended Slices in Python"
date:   2018-04-26 13:00:00 +0800
categories: 
---

In [a Leetcode practice](https://leetcode.com/explore/interview/card/top-interview-questions-easy/127/strings/879/), where I was asked to reverse the order of a string, my algorithm beat 97.49% of Python3 submissions. This is satisfactory but I was curious about what the top algorithm did, so I took a peek:

```
s[::-1]
```

This is highly efficient! What looks mysterious and confuses us is that this seemingly applies some kind of slicing that is suitable for 2D arrays but not for 1D arrays. Amazingly, the last _"index"_ doesn't not represent slicing but **steps**. Then all looks reasonable and obvious.

References:

- [15 Extended Slices](https://docs.python.org/2.3/whatsnew/section-slices.html)