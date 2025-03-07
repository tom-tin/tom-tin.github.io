---
layout: post
title:  "Explainable ML: Overview"
date:   2025-03-07 11:00:00 +0700
categories: [ai, explain]
---

- [LIME: Local Interpretable Model-agnostic Explanations](https://www.facebook.com/groups/pypcom/permalink/2499990443671343/?mibextid=wwXIfr&rdid=Aye18LIM2Nn2ZIDE&share_url=https%3A%2F%2Fwww.facebook.com%2Fshare%2Fp%2F1DW1et1Rqs%2F%3Fmibextid%3DwwXIfr#)
  - to estimate the local variations of a prediction by perturbing the feature values of the specific data instance
  - LIME works a bit differently for different data types:
    - For tabular data, we can perturb the feature by simply adding some small noise to the continuous variables. For categorical variables, it is more delicate as the concept of distance is more subjective. Another way to do it is to choose another value of the feature from the dataset.
    - For text data, the features are usually the words or the tokens. The typical way to perturb the features is to remove at random a few words from the original sentence. It is intuitive to think that if we remove an important word, the predictions should change quite a bit.
    - For image data, pixels are not really representative of what "matters" in an image. "Super-pixels" are created by segmenting the image (clustering similar close pixels) and then serve as the main features. We can turn on and off those new features by zeroing their values. By turning off a few super-pixels, we effectively perturb the feature set enough to estimate which segments contribute the most to the predictions. 

