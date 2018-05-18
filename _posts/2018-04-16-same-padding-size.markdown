---
layout: post
title:  "Setting Parameters Right for Convolutional Layers with 'SAME' Padding"
date:   2018-04-16 22:03:33 +0800
categories: 
---

The typical way to calculate the output size of a convolutional layer is pretty straightforward:

```
(W−F+2P)/S+1
```

`W` stands for the width/height of the input shape;
`F` stands for the width and height of the filter window;
`P` is the number of paddings;
`S` is the stride, along a particular axis.

However, when the `SAME` padding is used, things get a little bit complicated because the output size is not only related to the paddings, but also to the **kernel size, original width and height, strides**. Fortunately, TensorFlow Documents provide us a convenient way to calculate the output size while `SAME` padding is used(also, while the `strides` is [2, 2]:

```
out_height = ceil(float(in_height) / float(strides[1]))
out_width  = ceil(float(in_width) / float(strides[2]))
```

Here the strides along both the vertical and horizontal direction are specified, though usually they are of the same value. It is convenient that the value of paddings is implicitly included in the calculation here.

# Still Need Help

If the implementation is urgent and you have no idea how to calculate the shape, just try the following line after the convolutional layer:
```
# say the convolutional layer you implemented is called conv1

conv1 = tf.layers.conv2d(x0, ...)

# Print the shape for manually tuning
print (conv1.get_shape().as_list())
```


References:

- [Convolutional Neural Network - TensorFlow](https://www.tensorflow.org/api_guides/python/nn#Convolution)

- [CS231n Notes on Convolutional Layer](https://cs231n.github.io/convolutional-networks/#conv)