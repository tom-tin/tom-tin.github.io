---
layout: post
title:  "Thompson Sampling"
date:   2025-08-03 09:00:00 +0700
categories: [reinforcement learning, Thompson Sampling]
---

## Expected rewards
### Beta prior
- If rewards are bounded (e.g., in [0,1]), can use Beta prior.
  - If our reward is an unbounded quantity, such as profit, we can first normalize it, then still apply Beta prior.
- Beta distr. is conjugate to the Bernoulli.
  - We are trying to estimate the probability that a campaign is "good" (i.e., profitable).
  - Hence, if we get feedback as a binary signal, we use Beta prior.
  - Beta distr. models the probability of sucess in a binary outomce (profit/non-profit).
- Parameters of Beta distr.
  - Both $\alpha, \beta > 0$ are real numbers, and are shape parameters (not scale parameters). This means they influence the shape of the curve without changing its range.
    - Higher $\alpha$: shift the peak of the distribution toward the right (closer to 1).
    - Higher $\beta$: shift the peak of the distribution toward the left (closer to 0).
    - Equal $\alpha, \beta$: When alpha and beta are equal, the distribution can be symmetrical (e.g., a U-shape when alpha and beta are less than 1, or a bell shape when they are greater than 1). When alpha and beta are both equal to 1, the distribution becomes a uniform distribution on. 
  - For the discrete case, you can use the following insight to help understand better 
    - $\alpha$: number of "successes" seen so far.
    - $\beta$: number of "failure" seen so far.
  - Mean $\mu = \frac{\alpha}{\alpha + \beta}$
  - Variance $\sigma^2 = \frac{\alpha \beta}{(\alpha + \beta)^2  (\alpha + \beta + 1)}$ --> deceases as we ahve more data.
- Process:
  - Initialize each arm with $\alpha=1$, $\beta=1$. Then, a Beta(1,1) is just a uniform distr. over [0,1].
  - Each round/day, we sample an "expected reward" of each arm from its Beta distr. (e.g. `np.random.beta(alpha, beta)`, then choose the arm with the highest sampled reward.
  - Then, we play that arm and observe its true reward (normalized) then update $\alpha, \beta$.
    - $\alpha += normalized_reward$
    - $\beta += 1 - normalized_reward$
- Python:
  - We can generate samples from Beta using: `samples_array = np.random.beta(5.6, 4.1, size=5)`, where $\alpha, \beta$ do not have to be integer.
