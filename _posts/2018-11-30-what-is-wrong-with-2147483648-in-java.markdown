---
layout: post
title:  "What is Wrong with Math.abs(-2147483648) in Java"
date:   2018-11-30 11:00:00 +0800
categories: 
---

The intuition about the value of `Math.abs(-2147483648)` should be `2147483648` undoubtedly, but it is not the case in Java, or perhaps any other C-based programming language.

The `int` type in Java is 32-bit, which means the largest integer it can store is 2147483647, or `Integer.MAX_VALUE`, and the smallest -2147483648, or `Integer.MIN_VALUE`. The number of `-2147483648` for an integer is perfectly fine, but the mathematical absolute value of -2147483648 is larger than the largest positive value Java integers can hold, which causes overflow.

In this case, you can imagine that the number axis is curved and forms a circle, where the maximum is now connected to the minimum. Since 2147483648 is **one** larger than 2147483647 and 2147483647 is actually the upper limit, the pointer now points at the minimum again, that is -2147483648.

This is why the in Java, `Math.abs(-2147483648)` or `Math.abs(Integer.MIN_VALUE)` is still `-2147483648`.

BTW, 2147483648 equals 2^31 and 2147483647 2^31-1, which adds up to 2^32. That's why 32-bit matters.

References:

- [Math.abs returns wrong value for Integer.Min_VALUE](https://stackoverflow.com/questions/5444611/math-abs-returns-wrong-value-for-integer-min-value)