---
layout: post
title:  "1 + 2 + \"3\""
date:   2018-11-30 12:00:00 +0800
categories: 
---

My intuition about `1 + 2 + "3"` is 54, because the character of "3" is of value 51 in the ASCII decimal table, which results in 54 while being added by 1 and 2.

But actually in Java, the `+` sign here, since there is a string in this operation, indicates that **cancatenation**, rather than **addition**, is happening here. The result of cancatenation of string and numbers if always string. It will be more obvious in this way:

`"The result of 1 + 1 is " + 2`

Thus, the answer to the question in the tile is "33", which is a string.