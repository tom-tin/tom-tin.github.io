---
layout: post
title:  "Hallucination"
date:   2025-02-19 06:00:00 +0700
categories: [ai, llms, hallucination]
---
Hallucinations happen when AI model generates content that is unrealistic, fictional, or completely fabricated.

## Stats
- [Hallucination Rate for Top 25 LLMs](https://github.com/vectara/hallucination-leaderboard). Varies from 0.7% to 30.0%.
  - First model to get below 1%: OpenAI-o3-mini-high-reasoning (0.8%).
  - From 1.3% to 2.0%: including Gemini-2.0-Flash, GPT-4o, GPT3.5 Turbo.
  - Model use to measure hallucination: HHEM-2.1.
 
## What causes Hallucination
- The model is not trained on enough data. (or not on recent data, using RAG helps).
- The model is trained on noisy or dirty data.
- The model is not given enough context.
- The model is not given enough constraints.
- It’s also due to the probabilistic nature of LLMs where error can propagate exponentially. (1-e)^n, where n is the number of tokens, and e is the error probability for each token. Even though e can be very small, but as n is very large then hallucination starts to happen. (Yan LeCun’s argument).
- Source: [At 14:21](https://www.youtube.com/watch?v=G2fqAlgmoPo)


## Some Ideas How to Reduce Hallucination
- Prompt Engineering: a technique to tweak the input so that the output matches your expectations.
- Fine-tuning pre-trained models: not a new trick (already existed in ML). Bad: increase training efforts. Good: reduce the cost of inference (since the cost of LLM APIs is dependent on input and output sequence length). So that you don’t have to provide examples in the prompt anymore.
- External data (RAG). FMs often lack of contextual info AND can become outdated quickly (e.g., GPT-4 was trained on data [before September 2021](https://openai.com/research/gpt-4)). This increases hallucination! Tools like [LlamaIndex (GPT Index)](https://gpt-index.readthedocs.io/en/latest/index.html), [LangChain](https://github.com/hwchase17/langchain), or [DUST](https://dust.tt/), available that can act as central interfaces to connect (“chaining”) LLMs to other agents and external data.
- Embeddings: Another way is to extract information in the form of embeddings from LLM APIs (e.g., movie summaries or product descriptions) and build applications on top of them (e.g., search, comparison, or recommendations). If [np.array](https://twitter.com/jeremyphoward/status/1647434956099186689) is not sufficient to store your embeddings for long-term memory, you can use vector databases such as [Pinecone](https://www.pinecone.io/), [Weaviate](https://weaviate.io/), or [Milvus](https://milvus.io/).
- Alternatives: As this field is rapidly evolving, there are many more ways LLMs can be leveraged in AI products. Some examples are [instruction tuning/prompt tuning](https://arxiv.org/abs/2104.08691) and model distillation.

## Resources
- [A good discussion on hallucination](https://www.facebook.com/groups/miaigroup/permalink/1560266621411271/?mibextid=I6gGtw). Most LLMs build their knowledge using Transformer - decoder only. The relationship between entities is represented using self-attention of the decoder block. How much it can learn depends on the number of parameters.
  - GPT-3: 175B. Google’s PaLM: 540B. GPT4: even more. But the more paras, the more stress on the infra like computing and training the models.
  - Argument: Maybe another architecture rather than Transformer-decoder only can help reduce size. Rightnow, with the above architecture, research shows that the bigger the LLMs, the better it will be.
  - For example, why don’t we switch back to the original Transformer architecture which have both Encoder and Decoder and use both to control for hallucination:
    - (1) bi-directional self-attention of encoder.
    - (2) cross-attention between encoder and decoder.
    - (3) self-attention of decoder.
  - In addition, by training multiple objective funcs simultaneously (e.g. masked language model, causal autoregressive) can help improve a few capabilities: document generation, zero-shot, few-shot.
  - These has been done by ViGPT.
- [Hallucination mitigation using agentic AI natural language-based frameworks](https://arxiv.org/pdf/2501.13946). Basically multiple AI agents can fact-checking each other to reduce hallucination. Theyy can exchange meta-informaiton. E.g. using 3 agents with a structured review process reduced hallucination scores by 96% across 310 test cases.
