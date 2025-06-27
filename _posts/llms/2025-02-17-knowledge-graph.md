---
layout: post
title:  "Knowledge Graph"
date:   2025-02-13 11:00:00 +0700
categories: [ai, llms, nlp, nn]
---

- [LLM Knowledge Graph Builder — First Release of 2025](https://neo4j.com/developer-blog/knowledge-graph-builder-first/)

### Knowledge Graph vs Graph Neural Network
| Aspect             | **Graph Neural Network (GNN)**                                           | **Knowledge Graph (KG)**                                                                  |
| ------------------ | ------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------- |
| **Definition**     | A neural network architecture that operates on graph-structured data     | A structured representation of knowledge in the form of entities and relationships        |
| **Input**          | Graphs with nodes, edges, and features (often numeric or categorical)    | Triples: (subject, predicate, object), like ("Product A", "is\_variant\_of", "Product B") |
| **Purpose**        | Learn representations (embeddings) for nodes, edges, or the entire graph | Store and query semantic information, often used for reasoning and inference              |
| **Learning?**      | Yes, end-to-end training using backpropagation                           | Not inherently "learning-based", though can be used alongside ML models                   |
| **Representation** | Dense vectors learned through message passing between nodes              | Symbolic, usually stored as RDF triples or a property graph (Neo4j, etc.)                 |
| **Examples**       | Node classification, link prediction, graph classification               | Entity linking, semantic search, recommendation                                           |
| **Applications**   | Social Nw analysis: Predict user behavior, friend recommendation. Molecule property prediction: For drug discovery (moledules as graphs) . Recommendation systems: Personalized recommendations by modeling user-item interaction graph. Fraud detection: Detect anomalies in transaction networks.      | Search engines: Google’s Knowledge Panel (e.g., “Barack Obama → Born In → Hawaii”). Chatbots & QA systems: Semantic understanding and retrieval. Product information management: Unified representation of items and their relationships. Personalization engines: Capture customer interests and intent                                           |

