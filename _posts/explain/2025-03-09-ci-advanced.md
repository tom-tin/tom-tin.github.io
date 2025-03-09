---
layout: post
title:  "Causal Inference - Advanced"
date:   2025-03-09 11:00:00 +0700
categories: [causal inference, explain]
---

## Ref
- (2023). Dynamic causal effects evaluation in a/b testing with a reinforcement learning framework.
  - Related to SUTVA method.
  - Develop online experiment methods in the presence of interference (effect over time, rather than across units).
    - A single unit in an experiment receives a series of treatments over time.
  - There are at least three major challenges in practice:
    - (i)    Accounting for the carryover effect when establishing causal inference.
    - (ii)   Implementing sequential hypothesis testing to stop the experiment once a stopping rule is reached, due to time and budget constraints.
    - (iii)  Designing the testing procedure to allow for adaptive treatment assignment.
  - How authors propose solutions:
    - Introduce a RL framework to solve (i)
    - They propose a sequential testing procedure to detect differences between two value functions, addressing the challenges outlined in (ii) and (iii).
      - The proposed test combines reinforcement learning and sequential analysis, enabling sequential monitoring and online updating.
    - The authors’ proposal tackles a crucial business challenge for ride-sharing companies (Uber).
