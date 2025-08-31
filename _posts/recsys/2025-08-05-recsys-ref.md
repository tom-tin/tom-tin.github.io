---
layout: post
title:  "Recommendation System - Resources"
date:   2025-08-05 09:00:00 +0700
categories: [ML, AI, RecSys]
---

## Models
### LightFM
* **A hybrid approach** that has adv from both collaborative and content-based filtering.
* **Flexibile**: Can incorporates metadata such as user preferences or item attributes.
* **Scalable**: Ok for large dataset (millions of users and items) (Python implementation). Optimized for sparse data.
* **Customizable**: Can use multiple loss functions:
  * Bayesian Personalized Ranking (BPR)
  * Weighted Approximate-Rank Pairwise (WARP)
* **Interpretable**: Clear separation between user/item embeddings --> help debugging and understanding.
* Industry examples:
  * Ecommerce: Personalized product recommendations (e.g., Amazon, Flipkart).
  * Streaming Platforms: Movie, music, content suggestions (e.g., Netflix, Spotify).
  * EdTech: Course or book recommendations tailored to users.
  * Healthcare: Personalized wellness plans or medication suggestions.
  * Hospitality: Travel or hotel recommendations based on user profiles. 
* Ref:
  * [LightFM in Action: AI Recommendations with Python](https://www.pysquad.com/blogs/lightfm-in-action-ai-recommendations-with-python).
  * [Building a Recommendation System with LightFM](https://medium.com/@murattyldrm7/building-a-recommendation-system-with-lightfm-35394c8d90fb)
  * [Recommendation System in Python: LightFM](https://towardsdatascience.com/recommendation-system-in-python-lightfm-61c85010ce17/) (Step-by-step guide)

## References
- [Ecommerce-Recommender-System-On-Aws-With-Mlops](https://github.com/nguyenthai-duong/Ecommerce-Recommender-System-On-Aws-With-Mlops)
