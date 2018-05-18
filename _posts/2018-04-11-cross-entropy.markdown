---
layout: post
title:  "Cross Entropy"
date:   2018-04-11 14:30:33 +0800
categories: 
---

Cross entropy is often used to calculate the loss of a classification model.

## Cross Entropy Function

The cross entropy is a calculation between two different probability distributions. In this example, the two distribution would be _p_ and _q_, which respectively stands for the "true" distribution and the "prediction" distribution.

![The cross entropy for the distributions {\displaystyle p} p and {\displaystyle q} q over a given set](https://wikimedia.org/api/rest_v1/media/math/render/svg/80bd13c723dce5056a6f3aa1b29e279fb90d40bd)

In the function above, note that the first parameter of **_H_** and the subscript of **_E_** indicates that, in this function, the "true" distribution is _p_ rather than _q_.

## Log loss

__Cross-entropy loss__, aka __log loss__, indicates the performance of a classification model, of which the output values is a probability between 0 and 1.

Usually 1 repersents that label of the data from the "true" distribution.

When the prediction diverges from the true label, say the model's prediction is close to 0 but the true label is 1, the loss would increase. In the graph below, in which case the label is 1, the log loss would increase if the prediction diverges from the true label of 1, and decreases while the prediction moves to the true label of 1.

![Log loss of predictions when true label is 1](http://ml-cheatsheet.readthedocs.io/en/latest/_images/cross_entropy.png)


References:

- [Cross Entropy - Wikipedia](https://en.wikipedia.org/wiki/Cross_entropy)

- [Loss Functions - ML Cheatsheet](http://ml-cheatsheet.readthedocs.io/en/latest/loss_functions.html#cross-entropy)

- [What is cross-entropy?
 - StackOverflow](https://stackoverflow.com/questions/41990250/what-is-cross-entropy?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa)