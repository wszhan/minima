---
layout: post
title:  "Preprocess Your Batches with NumPy.split Function"
date:   2018-04-09 15:50:33 +0800
categories: 
---

![NumPy](https://secure.meetupstatic.com/photos/event/b/4/9/3/600_463786227.jpeg)

The NumPy.split() function is pretty useful why you want to turn a 1-d array into a desired shape.

It takes a while to understand but it is totally worth it.

The documentation for this function is always better than any other explanation, check it [here](https://docs.scipy.org/doc/numpy/reference/generated/numpy.split.html).

I was using this function to preprocess data into mini-batches for Recurrent Neural Network. The original data is quite complicated, let's use a simple case here.

Say my text is:
```
Split an array into multiple sub-arrays of equal or near-equal size. Does not raise an exception if an equal division cannot be made.
```

After removing the duplicate vocabulary and with some magic, the text has been turned into a list:
```
# 20 unique words
int_text = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20]
```

And I want my data to be arranged in this form:
```
batch_size = 3
sequence_length = 2
n_batches = len(int_text) // (batch_size * sequence_length) # 3

# Shape: (3, 2, 3, 2) = (n_batches, 2, batch_size, sequence_length) # 2 = 1 train + 1 target
[
  # First Batch
  [
    # Batch of Input
    [[ 1  2], [ 7  8], [13 14]]
    # Batch of targets
    [[ 2  3], [ 8  9], [14 15]]
  ]

  # Second Batch
  [
    # Batch of Input
    [[ 3  4], [ 9 10], [15 16]]
    # Batch of targets
    [[ 4  5], [10 11], [16 17]]
  ]

  # Third Batch
  [
    # Batch of Input
    [[ 5  6], [11 12], [17 18]]
    # Batch of targets
    [[ 6  7], [12 13], [18 19]]
  ]
]
```

This can be done with 3 ```for``` loops and about 15 lines of code.

But with NumPy.split(), te implementation is:
```
x = np.array(int_text[:n_batches * batch_size * sequence_length])
y = np.array(int_text[1:n_batches * batch_size * sequence_length+1]) # this is an RNN

x_batches = np.split(x.reshape(batch_size, -1), n_batches, 1)
y_batches = np.split(y.reshape(batch_size, -1), n_batches, 1)

batches = np.array(list(zip(x_batches, y_batches)))
```

Again, check the documentation for more surprises.