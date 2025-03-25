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
- **Assumptions**:
  - **Stable Unit Treatment Value Assumption (SUTVA)** – No interference between units.
  - **Unconfoundedness (Conditional Independence)** – No unmeasured confounders.
  - **Common Support (Overlap Condition)** – Sufficient overlap in covariates between treated and control groups.
  - **For DiD**:
    - **Parallel Trends**: T and C groups would have evolved similarly without treatment (i.e. must have similar pre-treatment trends).
      - Example: If you're studying the impact of a minimum wage increase on employment, but the treated regions already had a declining employment trend before the policy change, the results may be misleading.
    - **No Anticipation**: Treatments doesn't affect the outcome before implementation.
      - Example: If businesses preemptively reduce hiring before a new minimum wage law takes effect, this would violate the assumption. 
    - **No Simultaneous Confounding Shocks**: No other event affects T/C groups differently at the same time.
      - Example: If a new tax policy was introduced at the same time as the minimum wage increase, it would be hard to separate their effects on employment. 
    - **Stable Composition of Groups**: No selection bias or differential attrition or migration. This ensures that differences are due to treatment, not changes in group characteristics.
      - Example of violation: If user self-select in to T group. If higher-skilled workers move out of states with a minimum wage increase, the observed employment effects might be due to worker mobility, not the policy itself.

### **B. Structural Causal Models (SCMs, Pearl’s Causal Graphs)**
- **Concept**: Uses Directed Acyclic Graphs (DAGs) to model causal relationships explicitly.
- **Key Methods**:
  - **Do-Calculus** – Adjusts for confounding using causal graphs.
  - **Instrumental Variables (IV)** – Uses external factors to estimate causal effects when treatment is endogenous.
  - **Front-Door Adjustment** – Identifies causal effects using mediators.
- **Assumptions**:
  - **Causal Sufficiency** – The DAG correctly represents the causal relationships.
  - **Instrument Validity (for IV)** – Instrument affects the outcome only through treatment. This entails 2 assumptions below. We say that an IV is valid if it satisfies both.
    - **Relevance** - The IV must be strongly correlated with the treatment. This is so that the IV can generate enough variation in the treatment. If not, we have a "weak IV bias". 
    - **Exclusion Restriction** – No direct or other indirect path from instrument to outcome.
    - Explain these two by example: Study the effect of education on income (target). Here, education is expressed by number of years for schooling (treatment).
      - If choose IV = distance to the nearest college: Exclusion assumption is violated, since living near a college also improves networking opportunities or access to better jobs independent of schooling.
      - If choose IV = education reform laws: Might be possible, since it can affect the treatment and not likely to affect income directly. 

### **C. Regression-Based Approaches**
- **Concept**: Uses statistical models to control for confounders and estimate causal effects.
- **Key Methods**:
  - **Ordinary Least Squares (OLS) with Covariate Adjustment** – Assumes no unobserved confounders.
  - **Fixed Effects Models** – Removes unit-specific biases by differencing within units over time.
  - **Synthetic Control Method** – Creates a weighted combination of control units to estimate counterfactual outcomes.
- **Assumptions**:
  - **Linearity (for OLS)** – Relationship between treatment and outcome is linear.
  - **No Time-Varying Confounders (for Fixed Effects)** – Confounders do not change over time.
  - **Parallel Trends (for Synthetic Control)** – Control units evolve similarly to the treated unit before treatment.

### **D. Machine Learning-Based Approaches**
- **Concept**: Uses ML to improve causal effect estimation.
- **Key Methods**:
  - **Causal Forests (Generalized Random Forests)** – Uses random forests to estimate heterogeneous treatment effects.
  - **Double Machine Learning (DML)** – Uses ML to flexibly control for confounders while maintaining valid inference.
  - **Uplift Modeling** – Predicts differential treatment effects at the individual level.
  - **Deep Causal Models** – Uses deep learning for estimating complex causal relationships.
- **Assumptions**:
  - **Unconfoundedness (for Causal Forests, DML)** – No unobserved confounders.
  - **Correct Model Specification (for ML methods)** – Models must be properly tuned and validated.
  - **Sufficient Data (for Deep Learning)** – Large datasets are needed to avoid overfitting.

---

## **2. Comparison of Causal Inference Models**

| **Method**                  | **Pros** | **Cons** | **Best Use Cases** | **Key Assumptions** |
|-----------------------------|---------|---------|------------------|------------------|
| **RCTs** | Strong causal claims, unbiased estimates | Expensive, ethical constraints | Clinical trials, policy evaluation | Randomization, SUTVA |
| **Matching (PSM, NN)** | Intuitive, improves balance | Requires good overlap, may not remove hidden confounders | Observational studies with rich covariates | Unconfoundedness, Common Support |
| **IPW** | Flexible, handles multiple covariates | Sensitive to extreme weights, requires correct model specification | Economics, healthcare, social sciences | Correctly specified propensity scores |
| **DiD** | Controls for time-invariant unobservables | Requires parallel trends assumption | Policy impact evaluation, labor economics | Parallel Trends, SUTVA |
| **SCMs (DAGs, Do-Calculus)** | Explicit causal assumptions, systematic | Requires correct causal graph | Epidemiology, econometrics, AI fairness | Causal Sufficiency |
| **IV** | Solves endogeneity issues | Needs a valid instrument, weak IV bias | Economics, pricing, labor studies | Instrument Validity, Exclusion Restriction |
| **Front-Door Adjustment** | Works when confounding is unavoidable | Needs a valid mediator | Mediation analysis, marketing attribution | Proper Mediator Selection |
| **OLS with Covariates** | Simple, interpretable | Fails if unobserved confounders exist | General observational studies | Linearity, No Unobserved Confounders |
| **Fixed Effects Models** | Removes time-invariant bias | Cannot control for time-varying confounders | Panel data studies | No Time-Varying Confounders |
| **Synthetic Control** | Robust for policy evaluation | Requires good donor pool | Public policy, regional studies | Parallel Trends |
| **Causal Forests** | Estimates heterogeneous effects | Hard to interpret, data-hungry | Personalized medicine, A/B testing | Unconfoundedness |
| **Double ML** | Strong theoretical guarantees | Sensitive to ML model choices | High-dimensional data, causal discovery | Unconfoundedness, Correct Model Specification |
| **Uplift Modeling** | Optimizes interventions | Needs large data, may overfit | Marketing, personalized recommendations | Proper Stratification |
| **Deep Causal Models** | Captures non-linearities | Opaque, requires large data | Healthcare, complex policy modeling | Sufficient Data, Correct Model Specification |

---

### **3. Choosing the Right Method**
- If you have **randomized data** → **RCTs**.
- If dealing with **observational data**:
  - **Matching/IPW** if confounders are well-measured.
  - **DiD/Fixed Effects** if longitudinal data is available.
  - **SCMs (DAGs, IV)** if confounding is complex.
  - **Machine Learning (Causal Forests, Double ML)** if high-dimensional data and heterogeneity matter.
 
### **4. Additional Notes**
- CUPED is a part of RCT framework, rather than observational methods like DiD or IV.
