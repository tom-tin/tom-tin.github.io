---
layout: post
title:  "ML Design Notes"
date:   2025-03-13 09:00:00 +0700
categories: [system, ml, design]
---

## System Design & Architecture
* **How would you design a scalable ML system for real-time inference?**
  * A scalable real-time ML system needs to optimize **latency, throughput, and fault tolerance**. My approach includes:
  * **Data Ingestion**: Use a high-throughput event-driven pipeline (Kafka, Pulsar).
  * **Feature Store**: Serve precomputed features with low-latency lookup (Feast, Redis).
  * **Model Serving**: Deploy models using **TensorFlow Serving, TorchServe, or Triton**. Use **ONNX** for cross-framework compatibility.
  * **Scalability**: Use **horizontal scaling** with Kubernetes and **auto-scaling** based on request load.
  * **Caching & Optimization**: Implement **model quantization (TFLite, FP16/INT8)** and **caching (Redis, Memcached)** for frequent queries.
  * **Monitoring**: Track inference latency, prediction distribution, and model drift with **Prometheus + Grafana**. 
* **Can you describe the architecture of a past ML solution you built and how it handled data, model training, and deployment?**
* **What trade-offs do you consider when choosing between batch and real-time processing for ML pipelines?**

## MLOps & Model Deployment
* **How do you ensure the reliability and scalability of ML models in production?**
* **What tools and best practices do you recommend for CI/CD in ML workflows?**
* **How do you monitor ML models post-deployment to detect drift and ensure performance?**

## Data Engineering & Feature Engineering
* **How do you design a feature store for a company that runs multiple ML models?**
* **What strategies do you use to handle data quality issues in ML pipelines?**
* **How do you optimize feature selection and engineering for large-scale datasets?**

## AI Strategy & Business Impact
* **How do you align AI/ML initiatives with business objectives?**
* **Can you give an example of an AI/ML solution you designed that had a significant business impact?**
* **How do you balance innovation with the practicality of deploying AI solutions at scale?**

## Leadership & Collaboration
* **How do you work with software engineers, data engineers, and product teams to deliver ML solutions?**
* **Have you led a team of ML engineers or data scientists? What’s your leadership style?**
* **How do you handle technical disagreements when designing ML solutions?**
