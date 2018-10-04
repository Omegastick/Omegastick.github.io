---
layout: post
title:  "Learning to Trust Your Critic - Grokking GAE"
date:   2018-10-04 20:00:00 +0900
categories:
mathjax: true
---

I've spent longer than I care to admit using Generalised Advantage Estimation without really understanding it. While I knew how to write the code and tune the hyperparameters, I never understood *why* I used it beyond "It makes the agent learn better most of the time." It turns out there's a very intuitive explanation of exactly what it does, which doesn't require any complex maths or deep analysis.

There are plenty of great tutorials on *how* GAE works and analysing it from a mathematical perspective, but I never found *one* covers the intuition behind it. It wasn't until I built a little Jupyter Notebook to test out different hyperparameter values for a project I'm working on that it 'clicked' and everything became clear.

So, condensed into one sentence, here's how GAE makes your agent train better:

>GAE trusts your critic instead of relying purely on rewards.

Now, that might be enough for some of you, but I know some people are still scratching their heads, so I'll explain some more (with examples).

What does GAE do, exactly?
==========================

I'll give an example of when GAE is much better than regular advantage estimation.

If you want to follow along, here's the code I'm using:
```python
import numpy as np
def calculate_gae(rewards, values, gae_param):
    real_values = []
    advantages = []
    value_deltas = []
    gaes = []
    
    print(f"Values: {values}")
    print(f"Rewards: {rewards}")
    print(f"Lambda: {gae_param}")
    
    real_value = values[-1]
    gae = 0
    for i in reversed(range(len(rewards))):
        real_value = real_value + rewards[i]
        advantage = real_value - values[i]
        value_delta = rewards[i] + values[i + 1] - values[i]
        gae = gae * gae_param + value_delta
        real_values.append(real_value)
        advantages.append(advantage)
        value_deltas.append(value_delta)
        gaes.append(gae)
        
    real_values = list(reversed(real_values))
    advantages = list(reversed(advantages))
    value_deltas = list(reversed(value_deltas))
    gaes = list(reversed(gaes))
    
    for i, real_value in enumerate(real_values):
        print("---")                
        print(f"Empirical value: {real_value:.2f}")
        print(f"Advantage: {advantages[i]:.2f}")
        print(f"Value delta: {value_deltas[i]:.2f}")
        print(f"GAE: {gaes[i]:.2f}")
```

While today's example is quite simple, the above function is great for playing around with and seeing what's happening at each step of GAE calculation.

A quick reminder on how GAE works. If you set GAE's parameter lambda ($$\lambda$$) to 1, then $$\hat{A}{}^{GAE}$$ is simply the regular advantage we use in standard actor-critic algorithms. However, if you set $$\lambda$$ to 0 instead it uses the difference between the next value and the current value plus the reward ($$r_t+{\gamma}V(s_{t+1})-V(s_t)$$).

In practice, this means that if you take an action that the critic (which is outputting the value) thinks is good or bad, you are immediately rewarded or punished for it.

Let's consider an environment with sparse rewards. In this environment, the agent does something good (that it didn't know it could do before), but doesn't receive a reward yet because the rewards are sparse. Then, it messes up and undoes the good thing it did. The values might look like this: $$[0, 0, 10, 10, 0, 0]$$ and the rewards like this (because they are sparse): $$[0, 0, 0, 0, 0]$$

Naturally, we want to encourage the good thing it did and discourage the bad thing.

If we perform an update on the situation above, we get the following:

```
Values: [ 0  0 10 10  0  0]
Rewards: [0 0 0 0 0]
Lambda: 0.0
---
Empirical value: 0.00
Advantage: 0.00
Value delta: 0.00
GAE: 0.00
---
Empirical value: 0.00
Advantage: 0.00
Value delta: 10.00
GAE: 10.00
---
Empirical value: 0.00
Advantage: -10.00
Value delta: 0.00
GAE: 0.00
---
Empirical value: 0.00
Advantage: -10.00
Value delta: -10.00
GAE: -10.00
---
Empirical value: 0.00
Advantage: 0.00
Value delta: 0.00
GAE: 0.00
```

Here, `GAE` is used as to update the probabilities of the model so that positive GAE values make it more likely to pick the same actions and negatives make it less likely.

As we can see, if we just used the advantage ($$\lambda=1$$) the model would get punished for the two timesteps it spent in the *'unexpectedly good'* state, but isn't rewarded for getting into that state in the first place. This means it is less likely to screw up (because the action that undid the *'good thing'* are punished) but it is never rewarded for getting into the 'unexpectedly good' state in the first place. Secondly, the first timestep it spends in the 'unexpectedly good' state is punished too, even though it might not have done anything wrong.

Instead, if we use the value delta for this update, the action that put it into a good state is rewarded and the one that undid that action is punished.

Of course, this relies on a very good critic that knows the expected outcome of every situation perfectly, which is why we don't just use the value delta all the time. Realistically, our critic is imperfect and it's better to rely mostly on the actual returns than just the value delta. Hence why we use $$\lambda\approx0.95$$ for most situations.