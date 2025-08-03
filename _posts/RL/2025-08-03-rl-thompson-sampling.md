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
  - $\alpha$: number of "successes" seen so far.
  - $\beta$: number of "failure" seen so far.
  - Mean $\mu = \frac{\alpha}{\alpha + \beta}$
  - Variance $\sigma^2 = \frac{\alpha \beta}{(\alpha + \beta)^2  (\alpha + \beta + 1)}$ --> deceases as we ahve more data.
- Process:
  - Initialize each arm with $\alpha=1$, $\beta=1$. Then, a Beta(1,1) is just a uniform distr. over [0,1].
  - 
