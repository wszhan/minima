---
layout: post
title:  "Simultaneous Calculation along Various Dimensions in CNNs using tf.nn.moments()"
date:   2018-04-14 15:15:33 +0800
categories: 
---

It seems not difficult how to calculate means and variances along several dimensions at the same time, however, it can sometimes be confusing. So it is worth being explained a little bit.

A very important thing to note is that: though the number of data along one single dimension would be a few, CNN is almost always not very high-dimensional. As in the graph below, which is a typical CNN, the dimension of data is usually **[batch_size, width, height, channels]**. This is key to understand the calculation of means, variances as well as other statistics across various dimensions.

![CNN](https://upload.wikimedia.org/wikipedia/commons/6/63/Typical_cnn.png)

Let's take a simple example, say the data is:
```
# original shape: (3, 2)

d = [
[1,2],
[3,4],
[5,6]
]
```

The dimension of ```d``` is **[3, 2]**. If we want the mean and variance across the columns, that is, vertically, we are expecting the output to be
```
[
[mean_column_1, mean_column_2],
[variance_column_1, variance_column_2]
]
```
, which is reasonable. 

Thus, a tip to use ```tf.nn.moments``` would be:
* **if you want to calculate a statistic across dimension _i_, put this _i_ into the ```axes``` parameter.**

```
mean, variance = tf.nn.moments(x, [0])

print (mean)
[3 4] # means

print (variance)
[2 2] # variances
```

References:

- [tf.nn.moments - TensorFlow Documentation](https://www.tensorflow.org/api_docs/python/tf/nn/moments)