---
layout: post
title:  "What is num_units in TensorFlow LSTM Model?"
date:   2018-04-10 23:35:33 +0800
categories: 
---

>If you have not prior knowledge of Recurrent Neural Network, please check the following readings:
- [Recurrent neural network - Wikipedia](https://en.wikipedia.org/wiki/Recurrent_neural_network)
- [Recurrent Neural Networks](https://www.tensorflow.org/tutorials/recurrent)

>Definitely a course on RNNs might cover more necessary information. I recommend Andrew Ng's Deep Learning courses on Recurrent Neural Networks(also called **Sequence Models** in Prof. Ng's courses), which are available on YouTube.

**LSTM**, that is, **Long Short Term Memory**, model is currently the most widely used and common model in Recurrent Neural Network practice. TensorFlow is one of the most popular machine learning framework among developers. It thus makes sense for us to build LSTM models with TensorFlow.

But while implementing LSTM RNNs in TensorFlow, we have to specify the parameter ```num_units``` in many classes or methods. In this case, for example:
```
tf.contrib.rnn.BasicLSTMCell(num_units)
```

~~Visually, of a unfolded RNN model, it means the number of LSTM cells. In the example below, ```num_units``` means the number of the blue cells.~~ 

~~Conceptually, ```num_units``` represents the sequence length of your input data. For example, in RNNs for NLP, ```num_units``` is the length of each training instance.~~

![Unfolded basic recurrent neural network - Wikipedia](https://upload.wikimedia.org/wikipedia/commons/thumb/b/b5/Recurrent_neural_network_unfold.svg/1920px-Recurrent_neural_network_unfold.svg.png)

Here is a single LSTM cell:
![LSTM cell structure - Wikipedia](https://upload.wikimedia.org/wikipedia/commons/thumb/6/63/Long_Short-Term_Memory.svg/1594px-Long_Short-Term_Memory.svg.png)

~~One single unit would consists of an independent structure. In LSTMs the structure would be like:~~

Previously, I thought ```num_units``` represents the cells in the RNN, but after reading more posts, it seems that, in the context of TensorFlow, this particular parameter of ```num_units``` is actually the number of layers stacked vertically at a particular timestep(or at all time steps).

Jason Brownlee has written [a post particularly about this](https://machinelearningmastery.com/stacked-long-short-term-memory-networks/), with Keras implementaion of a single LSTM cell(or layer, depending on the context of framework).

According to [this thread on Google Groups](https://groups.google.com/a/tensorflow.org/forum/#!msg/discuss/74BrHpM76Q4/O4CwWOgfAgAJ) and [this issue posted on GitHub](https://github.com/tensorflow/tensorflow/issues/14693), it seems that the TensorFlow team has already noticed the inconsistency on this parameter name. But still it is used in the current version(at the time of this writing, the latest version for Mac OS is 1.7.0, either for CPU or for GPU), because of the need for backward compatibility. This is understandable but also erroneous. Even with backward compatibility kept intact, and nomenclature varies among researchers and developers, additional information could be added to the documentation to avoid inconsistency and misunderstanding.

References:

- [Understanding LSTM in Tensorflow(MNIST dataset)](https://jasdeep06.github.io/posts/Understanding-LSTM-in-Tensorflow-MNIST/)

- [TensorFlow documentation on ```tf.contrib.rnn.BasicLSTMCell```](https://www.tensorflow.org/api_docs/python/tf/contrib/rnn/BasicLSTMCell#methods)

- [What is num_units in tensorflow BasicLSTMCell?
](https://stackoverflow.com/questions/37901047/what-is-num-units-in-tensorflow-basiclstmcell?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa)

