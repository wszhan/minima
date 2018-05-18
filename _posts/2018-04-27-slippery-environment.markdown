---
layout: post
title:  "Slippery Environment"
date:   2018-04-27 17:00:00 +0800
categories: 
---

While doing some reading about _action value function_ with regards to evaluating the _policies_ in reinforcement learinng, I took for granted the certainty of this condition:

![Action Value Function]({{"/assets/action-value-func.png"}})

But this is not the case. This *action value* could highly possibly be unstable. This is very well illustrated in Open AI Gym Environment called [Frozen Lake](https://github.com/openai/gym/blob/master/gym/envs/toy_text/frozen_lake.py). Additional introduction about this environment is [here](https://gym.openai.com/envs/FrozenLake-v0/).

In this particular environment, there's an important attribute called `is_slippery`, which is a boolean value, either `True` or `False`. This attribute simulates a 'slippery ice ground', on which _"the ice is slippery, so you won't always move in the direction you intend"_. This means that, if you set `is_slippery` to be `True`, then even though a set state-action pair is input into the model, either one or several(up to 4 at most) could come out.

This is why in the pseudocode below, `Q(s, a)` is a sum of action values rather than just a value:
![Estimation of Action Values](https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59cc021b_est-action/est-action.png)

This is a very important point that I missed while reading about action value function previously.

References:

- [Conditional probability distribution](https://en.wikipedia.org/wiki/Conditional_probability_distribution)

- [Environments](https://gym.openai.com/envs/)

- [Open AI Gym - GitHub](https://github.com/openai/gym)

- [Frozen Lake Source Code](https://github.com/openai/gym/blob/master/gym/envs/toy_text/frozen_lake.py)