---
layout: post
title:  "Transformers"
date:   2025-08-05 09:00:00 +0700
categories: [ai, llms, transformers]
---

### Resources
- [On the Expressiveness of Softmax Attention: A Recurrent Neural Network Perspective](https://huggingface.co/papers/2507.23632)
  - Softmax attention has become the backbone of modern transformer architectures.
    - The nonlinearity is applied on the inner product of the query q and key k. 
    - Good: expressiveness, scalability.
    - Bad: quadratic memory and computational complexity vs sequence length.
  - Approach 1: replace SA by Linear form of attention --> but downstream accuracy suffers.
  - This paper helps break down SA into components that can be described in the language of RNNs --> helps explain why DA is more expressive than its counterparts.
- 
