---
layout: post
title:  "Causal Inference - Models Overview"
date:   2025-03-25 11:00:00 +0700
categories: [causal inference, explain, models, overview]
---

## **1. Causal Inference Models Overview**

### **A. Potential Outcomes Framework (Rubin Causal Model)**
- **Concept**: Each unit has a potential outcome for each possible treatment.
- **Key Methods**:
  - **Randomized Controlled Trials (RCTs)** – Gold standard for causal inference.
  - **Matching (Propensity Score Matching, Nearest Neighbor Matching)** – Matches treated and control units with similar characteristics.
  - **Inverse Probability Weighting (IPW)** – Weights units to balance treatment and control groups.
  - **Difference-in-Differences (DiD)** – Compares pre/post-treatment differences between treated and control groups.

### **B. Structural Causal Models (SCMs, Pearl’s Causal Graphs)**
- **Concept**: Uses Directed Acyclic Graphs (DAGs) to model causal relationships explicitly.
- **Key Methods**:
  - **Do-Calculus** – Adjusts for confounding using causal graphs.
  - **Instrumental Variables (IV)** – Uses external factors to estimate causal effects when treatment is endogenous.
  - **Front-Door Adjustment** – Identifies causal effects using mediators.

### **C. Regression-Based Approaches**
- **Concept**: Uses statistical models to control for confounders and estimate causal effects.
- **Key Methods**:
  - **Ordinary Least Squares (OLS) with Covariate Adjustment** – Assumes no unobserved confounders.
  - **Fixed Effects Models** – Removes unit-specific biases by differencing within units over time.
  - **Synthetic Control Method** – Creates a weighted combination of control units to estimate counterfactual outcomes.

### **D. Machine Learning-Based Approaches**
- **Concept**: Uses ML to improve causal effect estimation.
- **Key Methods**:
  - **Causal Forests (Generalized Random Forests)** – Uses random forests to estimate heterogeneous treatment effects.
  - **Double Machine Learning (DML)** – Uses ML to flexibly control for confounders while maintaining valid inference.
  - **Uplift Modeling** – Predicts differential treatment effects at the individual level.
  - **Deep Causal Models** – Uses deep learning for estimating complex causal relationships.

---

## **2. Comparison of Causal Inference Models**

| **Method**                  | **Pros** | **Cons** | **Best Use Cases** |
|-----------------------------|---------|---------|------------------|
| **RCTs** | Strong causal claims, unbiased estimates | Expensive, ethical constraints | Clinical trials, policy evaluation |
| **Matching (PSM, NN)** | Intuitive, improves balance | Requires good overlap, may not remove hidden confounders | Observational studies with rich covariates |
| **IPW** | Flexible, handles multiple covariates | Sensitive to extreme weights, requires correct model specification | Economics, healthcare, social sciences |
| **DiD** | Controls for time-invariant unobservables | Requires parallel trends assumption | Policy impact evaluation, labor economics |
| **SCMs (DAGs, Do-Calculus)** | Explicit causal assumptions, systematic | Requires correct causal graph | Epidemiology, econometrics, AI fairness |
| **IV** | Solves endogeneity issues | Needs a valid instrument, weak IV bias | Economics, pricing, labor studies |
| **Front-Door Adjustment** | Works when confounding is unavoidable | Needs a valid mediator | Mediation analysis, marketing attribution |
| **OLS with Covariates** | Simple, interpretable | Fails if unobserved confounders exist | General observational studies |
| **Fixed Effects Models** | Removes time-invariant bias | Cannot control for time-varying confounders | Panel data studies |
| **Synthetic Control** | Robust for policy evaluation | Requires good donor pool | Public policy, regional studies |
| **Causal Forests** | Estimates heterogeneous effects | Hard to interpret, data-hungry | Personalized medicine, A/B testing |
| **Double ML** | Strong theoretical guarantees | Sensitive to ML model choices | High-dimensional data, causal discovery |
| **Uplift Modeling** | Optimizes interventions | Needs large data, may overfit | Marketing, personalized recommendations |
| **Deep Causal Models** | Captures non-linearities | Opaque, requires large data | Healthcare, complex policy modeling |

---

### **3. Choosing the Right Method**
- If you have **randomized data** → **RCTs**.
- If dealing with **observational data**:
  - **Matching/IPW** if confounders are well-measured.
  - **DiD/Fixed Effects** if longitudinal data is available.
  - **SCMs (DAGs, IV)** if confounding is complex.
  - **Machine Learning (Causal Forests, Double ML)** if high-dimensional data and heterogeneity matter.
