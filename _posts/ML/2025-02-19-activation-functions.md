---
layout: post
title:  "Activation Functions"
date:   2025-02-19 05:00:00 +0700
categories: [ml, dl, activation]
---

## Why bother?
- To provide some non-linearity to the model --> allow it to learn more complex data.
- Hence, must be monotonic, differentiable, and quickly converging w.r.t the weights.

## Types
- **Sigmoid**: input: all real (-inf,+inf), output: [0,1].
  - Therefore, can represent the class probabilities.
  - Derivatives can be expressed i.t.o. the function itself.
- **Sofmax**:
  - For last layer of a DNN for multi-class classification.
  - Can have exponential float-overflow issues. One trick is to divide both num and deno by e^m where m=max(x1,...,xN). [Source](https://www.facebook.com/groups/viettechies/permalink/1367133101405032/?mibextid=wwXIfr&rdid=iqhfUKTBEHKD9uH6&share_url=https%3A%2F%2Fwww.facebook.com%2Fshare%2Fp%2F1BhFq4r3Ph%2F%3Fmibextid%3DwwXIfr#).
- **Tanh (Hyperbolic Tangent)**: output: [-1,1].
  - Derivatives can be expressed i.t.o. the function itself.
- **RELU (Rectified Linear Unit)**:
  - if the initial output is <0, then output 0. If not, do nothing to the initial output.
  - The formula max(0,z) is deceptively simple.
  - Same benefit as Sigmoid, but with better performance.
- **Leaky ReLU**:
  - Purpose is to fix the “dying ReLU” gradient problem.
  - When z<0, instead of output 0, it outputs a small, non-zero constant gradient alpha (normally, alpha=0.01). The performance consistency across tasks is still unclear.
- **Parametric ReLU**:
  - Let Neurons choose what slope is best in the negative region.
  - PReLU can become either ReLU or Leaky ReLU with certain values of alpha.
- **Maxout**:
  - a generalization of the ReLU and the leaky ReLU functions. It is a piecewise linear function that returns the maximum of inputs, designed to be used in conjunction with the dropout regularization technique. Both ReLU and leaky ReLU are special cases of Maxout.
  - The Maxout neuron, therefore, enjoys all the benefits of a ReLU unit and does not have any drawbacks like dying ReLU. However, it doubles the total number of parameters for each neuron, and hence, a higher total number of parameters need to be trained.
- **ELU (Exponential Linear Unit)**:
  - Converges faster, produces more accurate results.
  - Unlike other activiation functions, ELU has an extra alpha const, which is a positive number.
  - Similar to ReLU, except for negative inputs:
    - ELU smoothly slowly until its output equal to -alpha, while ReLU sharply smoothes.

## General Tips on what to choose
- Depends on the problem type, and the range of expected output.
- if want to predict value >1 🡪 use ReLU (can’t sigmoid or Tanh).
- if want to predict value in (0,1) or (-1,1) 🡪 don’t use ReLU.
- Classification to predict prob dist. Over mutually exclusive class labels 🡪 softmax in the last layer. If binary class 🡪 use Sigmoid in last layer.
  - In hidden layer, don’t use Sigmoid or Tanh.
  - In hidden layer, as a rule of thumb, use ReLU. Even better: Leaky ReLU. 

## New discoveries
- [Sigmoid Self-Attention is Better than Softmax Self-Attention: A Mixture-of-Experts Perspective](https://arxiv.org/abs/2502.00281).
  - Explain theoretically the advantages of using signmoid over softmax in the Attention mechanism in Transformer.
  - Inspired by the [Apple's paper](https://arxiv.org/abs/2409.04431) on the practical advantage of using sigmoid for Self-Attention mech.
  - Summary: using sigmoid makes training and inference faster and more stable than softmax.

## Resources
- [Activation Functions Neural Networks: A Quick & Complete Guide](https://www.analyticsvidhya.com/blog/2021/04/activation-functions-and-their-derivatives-a-quick-complete-guide/)
- [How to Choose an Activation Function for Deep Learning](https://machinelearningmastery.com/choose-an-activation-function-for-deep-learning/).
