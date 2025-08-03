---
layout: post
title:  "Thompson Sampling"
date:   2025-08-03 09:00:00 +0700
categories: [reinforcement learning, Thompson Sampling]
---

## Expected rewards
### Beta prior
- If rewards are bounded (e.g., in [0,1]), can use Beta prior.
- Process:
  - Initialize each arm with $\alpha=1$, $\beta=1$.  
