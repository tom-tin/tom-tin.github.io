---
layout: post
title:  "Reinforcement Learning Notes"
date:   2025-02-19 09:00:00 +0700
categories: [ai, reinforcement learning]
---

## Terminologies
- Off-Policy Evaluation (OPE): a technique in RL to estimate the performance of a target policy (i.e., the policy you want to evaluate) using data collected by a behavior policy (i.e., a different policy used to generate the data).
  - In other words, you can come up with a new policy A (e.g., using simulation). You want to evaluate how A would perform in a given scenario without having to directly execute A in the environment.
  - [A Review of OPE in RL](https://arxiv.org/pdf/2212.06355).
- 

## Limitations
- Real-time use can be limited.
  - Need a lot of interactions with the env. to learn effective policies.
  - Slow inference or policy updates for deep RL algos --> prevent applications in high-freq trading or robotics.
  - Rewards in RL are often delayed --> computational expensive esp. in dynamic env. where feedbackloops must be rapid.
  - Potential solution:
    - Use offline RL with past data to solve cold start problem
    - Use causal RL to extrapolate beyond the current policy
    - Use similated data from digital twins (esp. in Robotics) can help.
    - Also check out this post: [No-code LLM Fine-Tuning and Debugging in Real Time: Case Study](https://mltechniques.com/2024/09/22/no-code-llm-fine-tuning-and-debugging-in-real-time-case-study/).
