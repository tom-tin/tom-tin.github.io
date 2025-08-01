---
layout: post
title:  "Reinforcement Learning Notes"
date:   2025-02-19 09:00:00 +0700
categories: [ai, reinforcement learning]
---

## Terminologies
### Evaluation
- Off-Policy Evaluation (OPE): a technique in RL to estimate the performance of a target policy (i.e., the policy you want to evaluate) using data collected by a behavior policy (i.e., a different policy used to generate the data).
  - [More details](https://tom-tin.github.io/ai/reinforcement%20learning/2025/07/28/rl-ope.html). 
### Offline RL
- Conservative Q-Learning (CQL): prevent value overestimation outside the data support.
- Implicit Q-Learning (IQL): strong, simple, stable without importance sampling.
- TD3+BC / BCQ / BRAC / AWAC: if your action is continuous (budget value).
- FQI/FQE (Fitted Q Iteration/Evaluation): classical, strong baselines.

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
