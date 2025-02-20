---
layout: post
title:  "Adaptive Experimentation"
date:   2025-02-20 19:00:00 +0700
categories: [ai, adaptive, experiment]
---

- [Adaptivity and Confounding in Multi-Armed Bandit Experiments](https://djrusso.github.io/docs/contextual_bai.pdf).
  - Authors: Chao Qin, Daniel Russo
  - Summary: This paper explores a new model of bandit experiments where nonstationary contexts influence the performance of arms. It introduces "deconfounded Thompson sampling," which balances adaptivity and robustness, achieving efficiency in stationary instances while maintaining resilience in nonstationary scenarios.
- [A Comparison of Methods for Adaptive Experimentation](https://research.manchester.ac.uk/files/308357062/2207.00683v1.pdf).
 - Authors: Samantha Horn, Sabina J. Sloman.
 - Summary: This study compares three adaptive experimentation methods: Thompson sampling, Tempered Thompson sampling, and Exploration sampling. It evaluates their performance in terms of social welfare and estimation accuracy across various experimental waves, revealing insights into their relative effectiveness.
- Multi-Armed Bandit Problem [Github](https://github.com/shuishida/Multi-Armed-Bandit).
  - Author: Shu Ishida
  - Summary: This GitHub repository implements various multi-armed bandit algorithms, including epsilon-greedy and UCB algorithms. It serves as a practical resource for comparing different bandit strategies through simulation experiments.
  - Implementation follows the algorithms described in [Introduction to Multi-Armed Bandits](https://arxiv.org/pdf/1904.07272.pdf) by Aleksandrs Slivkins.
- [TS-GLR: an Adaptive Thompson Sampling for the Switching Multi-Armed Bandit Problem](https://hal.science/hal-03628791v1/document)
  - Authors: Réda Alami, Oussama Azizi
  - Summary: This paper presents a Thompson Sampling strategy equipped with a change point detector for nonstationary environments. It addresses the challenges posed by changing reward distributions and provides analytical results on regret minimization.
- [Using Multi-Armed Bandits to Conduct Adaptive Educational Experiments](https://files.eric.ed.gov/fulltext/EJ1220507.pdf)
  - Authors: Anna N. Rafferty, Huiji Ying, Joseph Jay Williams
  - Summary: This research investigates how multi-armed bandit algorithms can improve educational technology experiments by dynamically allocating students to conditions based on real-time data. It discusses the trade-offs between statistical reliability and student outcomes.
 

