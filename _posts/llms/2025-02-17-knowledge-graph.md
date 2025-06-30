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

#### Example Use Case 1: KG in E-commerce
**Business Problem**
An ecommerce company face:
* Product data inconsistency (e.g., same T-shirt under multiple SKUs for different colors).
* Customers searching for “black summer dress” get incomplete results.
* Hard to recommend complementary items (handbags with dresses, etc.).

**Solution**
Build a KG that can **connects related entities** to **unify and enrich product data**.

You can build a KG from the following input in the form of (subject, predicate, object):
~~~python
(SKU123, "is_variant_of", SKU456)
(SKU123, "has_color", "black")
(CustomerA, "purchased", SKU123)
(SKU123, "belongs_to", "summer collection")
(SKU123, "belongs_to", "dresses")
(SKU123, "frequently_bought_with", SKU456)
~~~
And then store it in Neo4j or Amazon Neptune for querying. 
This can help with:
* Semantic Search:
 * User types: "black cotton summer dress under $50"
 * The KG connects synonyms & related categories (e.g., "cocktail" → "party dress").
* Cross-sell & Up-sell:
 * Via paths connected with relationships: "purchased", "frequently_bought_with".
 * Then recommend handbags that were co-purchased.
* Product QA & Chatbots:
 * Answers questions like “What is the care instruction for this?” by linking to attribute nodes.

Tools used:
* Neo4j graph database to store and query KG.
* NLP pipelines to auto-extract relationships from product descriptions.
* Graph algorithms (like PageRank or community detection) to rank popular products in segments.

**Example Use Case 2**: GNN in E-commerce
**Business Problem**
The same ecommerce company wants to improve **personalized recommendations** beyond collaborative filtering.
They want to capture:
* Sequential clicks (session-based).
* Product-Product similarity (from user co-interactions).
* Social signals (influencer likes, etc.)

**Solution**
Use a GNN to predict the next likely purchase.

Graph Structure:
* Nodes: Customers, Products.
* Edges:
 * viewed, added_to_card, purchased.
 * Weighted by recency & frequency.

**Models**:
* GNN type: **GraphSAGE** or **GAT (Graph Attention Network)**.
* Task: **Link Prediction** (predict edge from a customer to new products).

**Results (Potential Impact)**:
* Improved CTR and conversion on recommendations by +12% over classic matrix factorization.
* More robust to cold-start: new products get embedded via graph strcuture.

**Tools used**
* PyTorch Geometric for GNNs.
* Features: Recency & Frequency of interactions, product category embeddings.
* Trained with historical sessions.

### References
#### Academic Papers
**Knowledge Graphs for E-commerce**:
* [Alibaba’s Product Knowledge Graph](https://arxiv.org/abs/2006.05688):  “Building a Product Knowledge Graph from E-commerce Websites”
* [Amazon Product Graph](https://dl.acm.org/doi/10.1145/3159652.3159672):  large-scale taxonomy & entity linking.

**Graph Neural Networks in Recommender Systems**:
* [PinSage (Pinterest’s large-scale GNN for recommendations)](https://arxiv.org/abs/1806.01973): 
* [Graph Neural Networks for Recommender Systems (survey)](https://arxiv.org/abs/2105.06339):.
* [Knowledge Graph Attention Network (KGAT) for recommendation](https://arxiv.org/abs/1905.07854):.


#### Libaries & Tools
* KG:
 * Neo4j, Amazon Neptune, Grakn, RDFLib (Python).
 * Stanford's Protege for ontology design.
* GNN:
 * [PyTorch Geometric](https://pytorch-geometric.readthedocs.io/):
 * [DGL (Deep Graph Library)](https://www.dgl.ai/):
 * TensorFlow GNN:

#### Blogs & Tutorials
* [Graph ML for recommendations (Pinterest)](https://medium.com/pinterest-engineering/graph-learning-at-pinterest-3f3bffb2f6c2):
* [Alibaba’s KG pipeline](https://tech.antfin.com/community/articles/784377):
* [GNN explained simply by Jay Alammar](https://jalammar.github.io/illustrated-graph-neural-networks/):
* [Neo4j E-commerce KG demo](https://neo4j.com/blog/tag/e-commerce/):

#### Open Code Examples
* [Session-based GNN recommendation (PyG)](https://github.com/CRIPAC-DIG/SR-GNN): Graph-based session recommendation)
* [KGAT implementation (RecBole)](https://github.com/RUCAIBox/RecBole): (standard toolkit with KG-enhanced recs)
