---
layout: post
title:  "InvalidArgumentError: Have you fed everything into the model?"
date:   2018-04-19 11:14:00 +0800
categories: 
---

Tips for you if you got the same error from the TensorFlow model: **check the `feed_dict` to make sure you _feed_ every required arguments and, which is equally important, the right arguments into the model**. There can be two possible problems:
- **Inputs missing(check [this post](https://github.com/tensorflow/tensorflow/issues/10632#issuecomment-307640692))**
- **Incorrect inputs fed into the model**. i.e. one function might want a rank 4 array with the first dimension being the number of training instances and a rank 3 array with the first dimension missed is passed into the model isntead.

Here is my case where I fed the wrong arguments into the model, which is even of a different shape from the required one.

Got the error:
```
...
InvalidArgumentError: You must feed a value for placeholder tensor 'Placeholder' with dtype float
	 [[Node: Placeholder = Placeholder[dtype=DT_FLOAT, shape=[], _device="/job:localhost/replica:0/task:0/cpu:0"]()]]

Caused by op 'Placeholder', defined at:
  File "/Users/ws/anaconda/envs/dlnd/lib/python3.6/runpy.py", line 193, in _run_module_as_main
    "__main__", mod_spec)
...
```

I could have missed something that I should feed into the model. So I check where the `feed_dict` throws the error:
```
                    train_loss_g = sess.run(g_loss, feed_dict={
                        inputs_real: batch_images,
                    })
```

This indicates that my `g_loss` is not fed properly. My `g_loss` comes from the function `model_loss`:
```
def model_loss(input_real, input_z, out_channel_dim):
    g_model = generator(input_z, out_channel_dim)
    
    d_model_real = discriminator(input_real)
    d_model_fake = discriminator(g_model, reuse=True)
    
    d_loss_real = tf.reduce_mean(
        tf.nn.sigmoid_cross_entropy_with_logits(logits=d_model_real, labels=tf.ones_like(d_model_real))
    )
    d_loss_fake = tf.reduce_mean(
        tf.nn.sigmoid_cross_entropy_with_logits(logits=d_model_fake, labels=tf.zeros_like(d_model_fake))
    )
    d_loss = d_loss_real + d_loss_fake
    
    g_loss = tf.reduce_mean(
        tf.nn.sigmoid_cross_entropy_with_logits(logits=d_model_fake, labels=tf.ones_like(d_model_fake))
    )
    
    return d_loss, g_loss
```

It is obvious that, to get `g_loss`, the input `input_z` is mandatory, which is a rank 2 vector that is distributed randomly and uniformly.
```
batch_z = np.random.uniform(-1, 1, size=(batch_size, z_dim))
```
What I fed into the model is `batch_images` images, which is obviously rank 4. Thus I made this little change:
```
                    train_loss_g = sess.run(g_loss, feed_dict={
                        inputs_z: batch_z,
                    })
```

And the model works, though not with good results, which requires further fine-tuning.

Again, though not always, the error returned is useful for us to pinpoint where the problem is.

References:

- [Answer to #10632](https://github.com/tensorflow/tensorflow/issues/10632#issuecomment-307640692)

