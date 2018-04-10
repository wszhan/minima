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

But while implementing LSTM RNNs in TensorFlow, we have to specify the parameter ```num_units``` in many classes or methods.

Visually, of a unfolded RNN model, it means the number of LSTM cells. In the example below, ```num_units``` means the number of the blue cells.

![Unfolded basic recurrent neural network - Wikipedia](https://upload.wikimedia.org/wikipedia/commons/thumb/b/b5/Recurrent_neural_network_unfold.svg/1920px-Recurrent_neural_network_unfold.svg.png)

Conceptually, ```num_units``` represents the sequence length of your input data. For example, in RNNs for NLP, ```num_units``` is the length of each training instance.

One single unit would consists of an independent structure. In LSTMs the structure would be like:
![LSTM cell structure - Wikipedia](https://upload.wikimedia.org/wikipedia/commons/thumb/6/63/Long_Short-Term_Memory.svg/1594px-Long_Short-Term_Memory.svg.png)



References:

- [TensorFlow documentation on ```tf.contrib.rnn.BasicLSTMCell```](https://www.tensorflow.org/api_docs/python/tf/contrib/rnn/BasicLSTMCell#methods)

- [What is num_units in tensorflow BasicLSTMCell?
](https://stackoverflow.com/questions/37901047/what-is-num-units-in-tensorflow-basiclstmcell?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa)