---
layout: post
title:  "Large Training Losses in TensorFlow"
date:   2018-05-18 16:00:00 +0800
categories: 
---

It is strange to see that training losses exceed 100, not to mention 1,000. But what happened iin my model is:

```
...
Episode: 82 Total Reward: 11.0 Training Loss: 56.0438 Explore Prob: 0.8416
Episode: 83 Total Reward: 17.0 Training Loss: 64.7601 Explore Prob: 0.8401
Episode: 84 Total Reward: 14.0 Training Loss: 1201.3579 Explore Prob: 0.8390
Episode: 85 Total Reward: 13.0 Training Loss: 532.6025 Explore Prob: 0.8379
Episode: 86 Total Reward: 39.0 Training Loss: 58.9685 Explore Prob: 0.8347
Episode: 87 Total Reward: 18.0 Training Loss: 1252.1827 Explore Prob: 0.8332
...
```

Clearly something is wrong. After checking all inputs, I found the bug in the learning class. Try find the bug:
```
class QNetwork:
    def __init__(self, learning_rate=0.01, state_size=4, action_size=2, hidden_size=10, name="QNetwork"):
    		...
            self.loss = tf.reduce_sum(tf.square(self.targetQs_ - self.Q))

            # Optimizer
            self.opt = tf.train.AdamOptimizer(learning_rate).minimize(self.loss)
```

Usually we should use the mean value of accumulated error to evaluate the loss, but here I used `tf.reduce_sum` instead, which caused all the horror.

After I changed it to
```
            self.loss = tf.reduce_mean(tf.square(self.targetQs_ - self.Q))
```

Things are getting better:
```
...
Episode: 82 Total Reward: 19.0 Training Loss: 19.3070 Explore Prob: 0.8590
Episode: 83 Total Reward: 11.0 Training Loss: 13.0111 Explore Prob: 0.8581
Episode: 84 Total Reward: 15.0 Training Loss: 15.5777 Explore Prob: 0.8568
Episode: 85 Total Reward: 10.0 Training Loss: 26.8611 Explore Prob: 0.8560
Episode: 86 Total Reward: 32.0 Training Loss: 126.4053 Explore Prob: 0.8533
Episode: 87 Total Reward: 16.0 Training Loss: 149.4870 Explore Prob: 0.8519
...
```

(The oscillation is fine because we are implementing Deep Q-Learning, where the agent knows nothing about the environment.)