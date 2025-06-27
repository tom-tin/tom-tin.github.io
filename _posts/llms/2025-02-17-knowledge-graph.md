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
| **Tools & Libraries**     | PyTorch Geometric, DGL, TensorFlow GNN. Models: GCN, GAT, GraphSAGE, R-GCN, LightGCN     | Graph DBs: Neo4j, Amazon Neptune, RDFLib. Ontology tools: Protégé        |


In Ecommerce:

| Aspect             | **Graph Neural Network (GNN)**                                           | **Knowledge Graph (KG)**                                                                  |
| ------------------ | ------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------- |
| What they do       | Learn powerful embeddings over graphs (users–products, product–product similarity, etc.). Predict next product to buy, bundle offers, or cross-sell suggestions               | Unify information across systems (products, customers, categories, brands). Provide semantic reasoning (e.g., "Lingerie is a type of women's underwear"). Enable personalized recommendations, faceted search, and chatbots                                           |
| Example Use Cases       | Session-based recommendation: Use GNNs (e.g., GAT, GCN) to predict what user will click next. Fraud detection: Model user–transaction–device graph to flag suspicious behavior. User embedding learning: Capture deep user interests from interaction patterns. Link prediction: Identify potential connections like “also bought” or “co-viewed”             | Product enrichment: Build a KG linking SKUs → categories → attributes → usage occasions. Semantic search: "Show me affordable red dresses under $50" → link price, color, category. Customer interest graph: Track product interactions → build a user–product graph. Multi-language/catalog linking: Map equivalent products across locales                                           |

Example: You can build a KG from the following input in the form of (subject, predicate, object):
~~~python
(SKU123, "is_variant_of", SKU456)
(SKU123, "has_color", "red")
(CustomerA, "purchased", SKU123)
(SKU123, "belongs_to", "summer collection")
~~~
And then store it in Neo4j or Amazon Neptune for querying.


| Use Case                | Knowledge Graph           | Graph Neural Network               |
| ----------------------- | ------------------------- | ---------------------------------- |
| Entity Linking & Search | ✅ Yes                     | ❌ Not designed for this            |
| Recommendation Systems  | ✅ With rules              | ✅ With learning & embeddings       |
| Fraud Detection         | ❌                         | ✅ Especially on transaction graphs |
| Personalized Experience | ✅ With semantic relations | ✅ With behavior modeling           |
| Customer Segmentation   | ✅ Hierarchical structure  | ✅ Graph clustering                 |


**Combine GNNs + KGs for Advanced Applications:**
* Knowledge-Enhanced Recommendations:
  * Use KG as input for GNN (e.g., KGAT: Knowledge Graph Attention Network)
  * Products and users embedded into a semantic space for improved relevance
* Explainable AI:
  * Use KG paths to explain why a product was recommended: “Because you liked X, which is similar to Y”

