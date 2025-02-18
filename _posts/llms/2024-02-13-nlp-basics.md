---
layout: post
title:  "NLP - LLMs - Basics"
date:   2025-02-13 11:00:00 +0700
categories: [ai, llms, nlp, nn]
---

## Reasoning LLMs
- [Understanding Reasoning LLMs](https://sebastianraschka.com/blog/2025/understanding-reasoning-llms.html) - Methods and Strategies for Building and Refining Reasoning Models.


## LLMs Explaining
- [LLM Visualization](https://bbycroft.net/llm). A great website to show how LLM works.

## Transformers Explaining
- [Explaining Transformers as Simple as Possible through a Small Language Model](https://pub.towardsai.net/explaining-transformers-as-simple-as-possible-through-a-small-language-model-6e6038941ca7)
- [How Transformer LLMs Work](https://www.deeplearning.ai/short-courses/how-transformer-llms-work/) (course by DeepLearning.AI). Instructor: Jay Alammar, Maarten Grootendorst.

## LSTM Explaining
- Specifically designed to avoid the vanishing and exploding gradients problem.
  - Thanks to a gated structure and the "constant error carousel" (where the backpropagation of the errors can decay slowly over many steps).   
- The gated structure is to control information flow. Gates: forget, input, output.
- It contrasts long-term memory (cell state c) vs. short-term memory (hidden state h).
- It mitigates the vanishing gradients problem through the "constant error carousel".
- Understand LSTM before learning about Transformers.
- Limit: due to seq2seq, encoder are separated from decoder --> can not scale.
- What makes Transformers better: they overcame the sequential processing limitations of RNNs/LSTMs. This enables MUCH faster training through GPU parallelization.
- LSTM is also the bridge between NLP and forecasting.

## LSTM Resources
- Understanding the LSTM Layer. [Linkedin post](https://www.linkedin.com/feed/update/groupPost:961087-7290418174666162177/).
- [Stanford course CS224N: NLP with DL](https://web.stanford.edu/class/cs224n/).

