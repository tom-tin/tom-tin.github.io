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
  * At company A,  I designed an **AI-powered anomaly detection system** for cloud infrastructure monitoring.
  * **Pipeline**:
   * Data streamed from logs via **Kafka** → Processed in **Spark** for batch & real-time feature extraction.
   * Model trained with **AutoML (HPO using Optuna)** and deployed via **TorchServe**.
   * Real-time inference in a **Flask/FastAPI service** with a Redis cache to reduce latency.
   * Anomaly alerts sent to monitoring dashboards (Prometheus, Grafana) and auto-healing actions triggered via webhooks.
  * **Scalability**:
   * Used **Kubernetes + Istio** for load balancing & traffic control.
   * Implemented **multi-armed bandits** to select the best anomaly detection model dynamically.

* **What trade-offs do you consider when choosing between batch and real-time processing for ML pipelines?**
  * **Latency vs. Accuracy**: Real-time processing prioritizes low latency, but batch jobs can use more complex models.
  * **Cost vs. Freshness**: Real-time systems require high **compute + storage costs** (e.g., AWS Lambda vs. EMR batch jobs).
  * **Complexity**: Streaming pipelines (Flink, Kafka Streams) are harder to manage than batch ETL jobs.
  * **Example**: In fraud detection, we use a **hybrid approach**—fast heuristic-based real-time scoring + deeper batch model retraining.

## MLOps & Model Deployment
* **How do you ensure the reliability and scalability of ML models in production?**
  * **CI/CD for ML**: Use **MLflow** to track versions, retrain triggers, and deploy models.
  * **Model versioning**: Serve multiple model versions (A/B testing, canary deployments).
  * **Infrastructure**: Deploy via **Kubernetes** with **horizontal auto-scaling**.
  * **Fault tolerance**: Use fallback models, graceful degradation mechanisms.
  * **Monitoring**: Log model predictions, monitor concept drift (EvidentlyAI), and alert on performance degradation.

* **What tools and best practices do you recommend for CI/CD in ML workflows?**
  * **Code Versioning**: Git + DVC (Data Version Control).
  * **Pipeline Automation**: Use **Kubeflow Pipelines** or **Metaflow**.
  * **Continuous Training**: Auto-retrain on new data with feature drift detection.
  * **Testing**: Unit test ML code (pytest), test model accuracy with holdout datasets before deployment.
  * **Deployment**: Use **Terraform for IaC**, Docker, and K8s for scalable model deployment.

* **How do you monitor ML models post-deployment to detect drift and ensure performance?**
  * **Concept & Data Drift**: Compare input distribution over time (EvidentlyAI, WhyLabs).
  * **Performance Tracking**: Log inference latency, accuracy decay, prediction skew.
  * **Retraining Triggers**: Automate retraining based on drift detection.
  * **Alerting**: Set up alerts on **Prometheus + Grafana** for unusual prediction patterns.
  * Versioning: Use time-travel queries to backtest models on past feature values.
 
* **What factors determine your choice of serverless vs server-based deployment?**
| **Criteria**           | **Serverless**                            | **Server-Based**                         |
|----------------------|--------------------------------|--------------------------------|
| **Inference Frequency** | Infrequent, unpredictable   | High and consistent traffic    |
| **Latency Requirements** | Acceptable with cold starts | Requires low-latency inference |
| **Scalability Needs** | Auto-scales instantly       | Requires manual/auto-scaling setup |
| **Cost**             | Pay-per-use, cost-effective | Higher fixed costs |
| **Hardware Needs**   | Limited GPU/CPU options     | Full hardware control (GPUs, TPUs) |
| **Operational Overhead** | Minimal (managed by provider) | Requires DevOps and maintenance |
| **Execution Time**   | Short-lived tasks           | Long-running tasks |


## Data Engineering & Feature Engineering
* **How do you design a feature store for a company that runs multiple ML models?**
  * **Online vs. Offline Features**: Use **Feast**—batch store in BigQuery, online store in Redis.
  * **Consistency**: Ensure **feature parity** across training and serving.
  * **Caching**: Frequently used features should be cached to reduce compute costs.
  * **Versioning**: Use **time-travel queries** to backtest models on past feature values.

* **What strategies do you use to handle data quality issues in ML pipelines?**
  * **Data Validation**: Use **Great Expectations** for schema validation.
  * **Missing Values**: Use **imputation (KNN, MICE)** or synthetic data generation (SMOTE).
  * **Anomaly Detection**: Auto-flag outliers using isolation forests.
  * **Data Drift Detection**: Track data distribution shifts with **Kolmogorov-Smirnov tests**.

* **How do you optimize feature selection and engineering for large-scale datasets?**
  * **Automated Feature Selection**: Use SHAP, LASSO, and PCA.
  * **Dimensionality Reduction**: Principal Component Analysis (PCA), Autoencoders.
  * **Feature Importance**: Use **XGBoost’s feature importance** to prune irrelevant features.
  * **Sparse Feature Encoding**: For categorical data, use **hashing tricks** or embeddings.

## AI Strategy & Business Impact
* **How do you align AI/ML initiatives with business objectives?**
  * Identify **key pain points** and define success metrics (ROI, latency, accuracy).
  * Collaborate with stakeholders to prioritize high-impact models.
  * Ensure AI solutions are explainable, reducing business risk.
  * Example: At company A, I designed an **ad ranking model** that increased ad CTR by **12%**, directly increasing revenue. 

* **Can you give an example of an AI/ML solution you designed that had a significant business impact?**
  * Built **personalized product recommendations** for an e-commerce client.
  * Used **hybrid collaborative filtering (ALS + Transformers)**.
  * A/B tested, saw **15% increase in conversion rates**. 

* **How do you balance innovation with the practicality of deploying AI solutions at scale?**
  * Use cutting-edge techniques, but prioritize **simplicity + maintainability**.
  * Example: Replaced complex **deep learning models** with an **XGBoost model** that performed **98% as well but was 5x faster** in inference. 

## Leadership & Collaboration
* **How do you work with software engineers, data engineers, and product teams to deliver ML solutions?**
  * Hold **cross-functional design reviews**.
  * Define **clear API contracts** between data pipelines and ML models.
  * Translate ML research into **production-ready code**.

* **Have you led a team of ML engineers or data scientists? What’s your leadership style?**
  * Yes, I lead with **mentorship, ownership, and technical depth**.
  * Encourage **knowledge sharing** and create a culture of **experimentation**.

* **How do you handle technical disagreements when designing ML solutions?**
  * **Data-driven approach**: Use A/B tests to validate decisions.
  * **Encourage open discussion**: Debate pros/cons objectively.
  * **Prioritize business impact**: Choose the simplest, most scalable solution.

