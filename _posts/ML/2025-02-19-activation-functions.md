---
layout: post
title:  "Activation Functions"
date:   2025-02-19 05:00:00 +0700
categories: [ml, dl, activation]
---

## New discoveries
- [Sigmoid Self-Attention is Better than Softmax Self-Attention: A Mixture-of-Experts Perspective](https://arxiv.org/abs/2502.00281).
  - Explain theoretically the advantages of using signmoid over softmax in the Attention mechanism in Transformer.
  - Inspired by the [Apple's paper](https://arxiv.org/abs/2409.04431) on the practical advantage of using sigmoid for Self-Attention mech.
  - Summary: using sigmoid makes training and inference faster and more stable than softmax.
