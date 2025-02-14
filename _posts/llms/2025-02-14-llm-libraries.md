---
layout: post
title:  "LLM Libraries"
date:   2025-02-14 11:00:00 +0700
categories: [ai, llms, tools]
---
# Libraries to access LLMs
- AI Suite (by Andrew Ng's team): [Github](https://github.com/andrewyng/aisuite).
  - Standardize API call for all models (instead of having to use SDK of each platform).
  - Easy to switch models with minimal code changes.
  - Easy model benchmarking: Can auto A/B test your AI app.
  - Easy API key management via env vars. Easy to set up.
  - Highlighted use cases:
    - Automated QA System: Use Mistral to create Q -> Use GPT-4 to answer -> Use Claude to eval.
    - Cost Optimization: Run a task on 3 models -> Compare cost/performance.  
