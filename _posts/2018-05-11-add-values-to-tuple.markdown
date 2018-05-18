---
layout: post
title:  "Add Values to Tuple in Python"
date:   2018-05-11 16:00:00 +0800
categories: 
---

It is easy to add values to list using `list.append()` method, but for tuples it would be a little bit more difficult because tuples are well-known for immutability.

However, though it might be impossible to add one single value, such as a floating number or integer, to tuples, adding tuples to tuples would be more convenient.

```
t1 = (1, 2, 3) # a tuple

# adding 4 to the end of the tuple
t1 = t1 + (4,)

print (t1)
# (1, 2, 3, 4)

```

This could be done for multiple reasons:
- This particular format `(4,)` creates a tuple immediately, which gives us a tuple for concatenation.
- The tuple is still immutable, we are just joining two tuples and assigning the new tuple to the original variable name. This sounds confusing but if you know the memory allocation in C you might understand why.

References:
- [how to add value to a tuple?](https://stackoverflow.com/questions/4913397/how-to-add-value-to-a-tuple)
