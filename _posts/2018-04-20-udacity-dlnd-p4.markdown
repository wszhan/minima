---
layout: post
title:  "Notes for Udacity DLND Project #4"
date:   2018-04-20 00:22:00 +0800
categories: 
---

As we are going further on the way of the Nanodegree, we must confront even more complex problems. To successfully conquer these problems, it is always critical to understand some basic but core concepts, as well as to be aware of some seemingly trivial but vital details. Here are some concepts/details should worth being noted.

## Image Data Input for the Discriminator

Here I made a mistake: `tf.tanh` was used as the activation function for the output of the generator, which is later fed into the discriminator. Meanwhile, the data yielded from the `get_batches` method that comes from the `Dataset` class of the `helper.py` file are used as the real input fed into the discriminator.

If we check the `helper.py` file and take a look at the `get_batches` method:
```
class Dataset(object):
    def __init__(self, dataset_name, data_files):
    	...

    def get_batches(self, batch_size):
    	...
            yield data_batch / IMAGE_MAX_VALUE - 0.5
```
, we will see the data is not only normalized, but also subtracted 0.5.

However, the `generator` function outputs data that ranges from -1 to 1.

Thus, this requires some treatment to the data yielded from the `get_batches` method.

## z and G(z)

`z` are vectors of noise. `G(z)` is the output from the generator function, which takes `z` as the input. It is important to tell the different between them. I wrote [a post]({{ site.baseurl }}{% post_url 2018-04-17-InvalidArgumentError-feed_dict %}) that is related to this issue.

## Why Leaky ReLu?

We don't want sparse gradients(~0 gradients), which could die out during backward propagation.

But the alpha could be low, which, while avoiding dying gradients, provides a slope close to 0 in the left half.

## Weight Initialization

This is not necessary but it really helps. I saw a lot of people missed it, yet the model still works, though outputing average results, as in my project.

## beta1

`beta1` is one of the _"Exponential decay rates for the moment estimates"_, as in [Kingma et al.](https://arxiv.org/abs/1412.6980). The default value of `beta1` is set to 0.9. But here you might need to think about a reasonable value to put in the model.



## Discriminator vs. Generator

According to [Salimans et al.](https://arxiv.org/abs/1606.03498), _"Training GANs consists in ﬁnding a Nash equilibrium to a two-player non-cooperative game"_. However, _"but we are not aware of any that are feasible to apply to the GAN game, where the cost functions are non-convex, the parameters are continuous, and the parameter space is extremely high-dimensional"_.

As a result, obvious from the plotting of losses for the discriminator and the generator, the discriminator outperforms the generator most of the time.

### Smoothing

In the `Intro_to_GANs_Solution.ipynb` of the **GAN_MNIST** exercise, the instructor says "To help the discriminator generalize better, the labels are reduced a bit from 1.0 to 0.9, for example, using the parameter smooth. This is known as label smoothing, typically used with classifiers to improve performance. In TensorFlow, it looks something like labels = tf.ones_like(tensor) * (1 - smooth)".

### Run the Generator Twice

This could be useful to give generator more chances to learn from the optimization, since here we are focusing on the generation of faces.

## Losses and Faces

Losses, both the `d_loss` and `g_loss`, in some sense indicate the performance of our model, but still could not help much. In some earlier trainings, I have been able to keep the generator loss stably under 1.0, while the discriminator loss varies between 1.0 and 2.0, depending on some minor modifications on the model. Here's an example:

![losses-1](https://i.imgur.com/lQJayCp.png)

But with this relatively reasonable losses comes these images:

![faces-1](https://i.imgur.com/aaTI9S7.png)

These pictures look weird and are still far away from satisfactory results, since you can easily tell they are fake.

## Training vs. Sampling

The model is always processing the data, but not always updating itself, this is why we include both `reuse` and `is_train` parameters into the model, to let the model know when it should update its weights and when it should not.

I did run the training session while I wanted to train the model; but I ran the session again without being specific about these flags while I was just sampling from the generator or calculating and saving the losses for plotting.

## Something that is mysterious but matters(seemingly)

While running the session of optimization, previously I used
```
sess.run(d_opt, feed_dict={
	inputs_real: batch_images,
	inputs_z: batch_z,
	lr: learning_rate,
	})
```

And my model always outputs weird images. Later, I re-checked the Udacity's solutions to the previous exercises, and added
```
_ = sess.run(d_opt, feed_dict={
                    inputs_real: batch_images,
                    inputs_z: batch_z,
                    lr: learning_rate,
                })
```

I have no idea why but this helps, a lot.

## Summary

It is very important to note that most of the time, possible improvements could be made not regarding the hyperparameters but regarding the model architecture. Before devoting your time to fine-tune the hyperparameters, make sure your model is implemented appropriately.

I used to be unconcerned with the 'black-box' of neural network, but now my mind might soon change. It is very important for researchers to understand how the neural networks work thus make it more efficient. Currently, some concepts are not intuitively useful, such as the losses of the generator and discriminator, which barely have anything to do with the realistic level of the output images. Developing an intuition about the architecture of the neural network in general and about the correlations among the parameters are essential to deep learning.

## Further Reading

These are not necessary for successfully completing this project, but it helps. I might do some writings on them in the future.

- [Wasserstein GANs](http://guimperarnau.com/blog/2017/03/Fantastic-GANs-and-where-to-find-them#wassGANs)

- [Wasserstein GAN](https://arxiv.org/abs/1701.07875)

- [TFGAN: A Lightweight Library for Generative Adversarial Networks](https://research.googleblog.com/2017/12/tfgan-lightweight-library-for.html)

- [Adam Optimizer](http://ruder.io/optimizing-gradient-descent/index.html#adam)


References:

- [Improved Techniques for Training GANs](https://arxiv.org/abs/1606.03498)

- [Adam: A Method for Stochastic Optimization](https://arxiv.org/abs/1412.6980)

- [Stability of Generative Adversarial Networks](http://www.araya.org/archives/1183)

- [InvalidArgumentError - Weisi Zhan]({{ site.baseurl }}{% post_url 2018-04-17-InvalidArgumentError-feed_dict %})