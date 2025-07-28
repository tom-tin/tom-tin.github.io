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
  - How it works: OPE methods typically use techniques like importance sampling to adjust the contributions of different actions and states in the historical data to account for the difference between A and B.
  - Why bother?
    - You can eval policies without executing them in the real world (useful in high risk / cost applications such as robotics, healthcare).
    - You can leverage existing data to gains insight into the performance of different strategies.
    - You can discover better policies than those used to generate the initial data.
    - 3 core methods in OPE:
    - Inverse Propensity Scoring (IPS): Reweight each logged sample based on how likely the new policy would have chosen the same action as the behavior (historical) policy did.
      - An example of importance sampling.
      - $V(\pi)$ is the expexcted reward (or value) if we were to run the new policy $\pi$ on the real environment. But since we can't directly sample from $\pi$ since all our logged data came from $\pi_b$, we need importance sampling.
      - Simply put, it is like replaying the historical dataset, but rescaling the importance of each datapoint depending on how relevant it is under the new policy.
    - Weighted Importance Sampling (WIS): Similar to IPS, but normalize the weights first to reduce variance.
    - Doubly Robust (DR) Estimator: Combine model-based and importance-weighted approaches.
      - Recall how the importance sampling approaches use 100% of weighted reward in final expected reward.
      - Here, we use only part of weighted reward. The rest come from a model that can learn/predict the expected reward.
      - Then you combine these two in the final expected reward.
    - If your historical data did not come from a particular policy (i.e., it is by rule-based), you don't have a behavior policy $\pi_b(a|s)$ to start with. But you can estimate this by:
      - Build a classification model to predict probability of an action given a state.
      - Remember to put softmax at output layer.
      - Now, you have an estimate $\pi_b(a|s)$ for any $(s,a)$
      - Then, use this to apply to IPS, WIS, DR.
      - Note that if your actions are continuous (e.g., real-valued budgets), you'll need to use kernel density estimators or discretize your action space.
    - If you don't want to estimate $\pi_b$, a practical alternative is to use Boostrapping.
      - Split hitorical data into train and validation/test campaigns.
      - Train your model (e.g., policy $\pi(a|s)$, or Q-value model).
      - On th test set, use your model to select the top action $\hat{a_i} = argmax_a Q(s_i,a)$ or $\pi(a|s)
      - Compare the actual observed rewards of:
        - Actions taken by the model.
        - Action taken historically.
      - Boostrapping:
        - Randomly resample the test data 1000 times.
        - Compute value estimates per resample.
        - Report:
          - Mean value estimate.
          - 95% CI.
          - Value uplift vs. baseline.    
- PPO 

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
