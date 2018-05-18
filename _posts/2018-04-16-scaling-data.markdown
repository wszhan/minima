---
layout: post
title:  "Normalize Data into Range of [0, 1] or [-1, 1]"
date:   2018-04-14 15:15:33 +0800
categories: 
---

While preprocessing data, we might want to data to be normalized in a certain range. Here are a few methods to normalize them into some useful and usual range:

## Scaling Data into [0, 1]

```
z = (x - min(x)) / (max(x) - min(x))
```

## Scaling Data into [-1, 1]

```
z = 2 * (x - min(x)) / (max(x) - min(x)) - 1
```

## Scaling data into [a, b]

```
z = (b - a) * (x - min(x)) / (max(x) - min(x)) + a
```

References:

- [How to normalize data to 0-1 range?](https://stats.stackexchange.com/questions/70801/how-to-normalize-data-to-0-1-range?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa)

- [How to normalize data between -1 and 1?](https://stats.stackexchange.com/questions/178626/how-to-normalize-data-between-1-and-1?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa)