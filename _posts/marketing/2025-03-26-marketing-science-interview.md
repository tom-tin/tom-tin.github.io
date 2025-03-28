---
layout: post
title:  "Marketing Science Interview"
date:   2025-03-26 17:00:00 +0700
categories: [marketing, interview]
---

## 1. How would you design an experiment to measure the effectiveness of a new advertising campaign?
- Use **A/B test (RCT)**. Steps:
- **Define Objectives & Key Metrics**:
  - Objective: Measure if the ad campaign drives an increase in **conversion rate** (e.g., sales, sign-ups) or **brand awareness**.
  - Metrics:
    - Conversion: conversion rate, CTR, Return on Ad Spend (ROAS)
    - Brand: Brand Lift (survey-based) 
  - **Randomize C and T groups**:
    - C: does not receive the new ad campaign.
    - T: receives the new ad campaign.
    - Ensure groups are statistically similar using random assignment.
  - **Experiment Duration & Data Collection**
    - Ensure **statistical power**.
    - Run the experiment long enough to avoid weekend or **seasonality effects**.
  - **Statistical Analysis**:
    - Use **t-tests** or **Bayesian inference** to check statistical significance.
    - If conversion rates are binary, use Chi-Square tests. (I think we can also use regression models).
    - If continuous, use ANOVA or **regression models**.
  - **Interpreting Results & Business Action**
    - If see statistically significant lift, recommend **scaling the campaign**.
    - If not, investigate **segment-wise performance** or potential external factors.

## 2. Can you discuss a time when your data analysis led to a significant change in a marketing strategy?
- **Scenario**: While working with an e-commerce client, they wanted to optimize ad spending but were unsure which channels drove the most conversions.
- **Problem**: The client allocated equal ad spend across: Google Ads, Fb Ads, Email Marketing. They also do this manually.
- **Approach**:
  - Used **MTA modeling** (Shapley Value & Markov Chains) to analyze conversion paths.
    - **Why Shapley Value**? A concept from cooperative game theory, to fairly allocate credit to each channel based on its **marginal contribution** to **all possible conversion paths**.
      - Treat each marketing channel as a player in a cooperative game.
      - Compute the **incremental contribution** of each channel by eval **all possible sequences of touchpoints**.
      - The final credit assigned to a channel is the **average marginal contribution** across all paths.
      - Work well with small datasets: Unlike deep learning-based attribution, Shapley is computationally feasible.
      - Interpretable results.
    - **Why Markov Chains**?
      - MC can model **user transitions** between marketing channels and help estimate the removal effect (what happens if a channel is removed).
      - Create a Transition Matrix:
        - Each marketing channel is a "state". The Prob of state transition is based on historical user paths.
      - Calculate Removal Effects.
        - Simulate removing a channel and measure how many conversion paths break.
        - The more paths disrupted, the move valuable the removed channel is.
      - Distribute Conversion Credit Based on Transition Probabilities.
        - Assign credit based on how often a channel helps move users forward in the journey.
      - MC can account for sequential behavior. Can learn from real data. Can handle complex conversion paths.
    - Note that both MTA models (Shapley or Markov Chain) can only show correlation rather than causality. Below, we suggest a way to establish causality.
  - Implemented **incremental testing** (**Geo Lift**) to isolate each channel's impact.
    - Geo Lift is an **experimental method** that measures **incremental impact** by **comparing regions where ads are active (treatment) versus regions where they are paused (control)**.
    - How it works:
    - Select Geographically Similar Regions (Matched Pairs).
      - Pick regions (cities, states, countries) that have similar **historical sales trend** and **consumer behaviors**.
      - E.g. If testing a Fb Ads campaign, find 2 cities that previously had **similar engagement and conversion rates**.
    - Run an A/B Test across Geo Locations: T (continue to see ads in selected regions). C (Pause ads in similar regions)
    - Measure the difference in Sales/Conversions.
    - Analyze Statistical Significance.
      - **DiD**
      - **Bayesian Structural Time Series (BSTS)** (advanced).
        - Predict the counterfactual: "What would have happened without ads?"
        - Control for seasonality and economic trends. 
        - Get confidence intervals for lift estimates. 
- **Findings**:
  - **Email Marketing had a 30% higher ROAS than Fb Ads**.
  - Fb Ads influenced top-funnel awareness but had **poor direct conversion**.
- **Business Impact**:
  - Recommended **reducing Fb spend by 20%** and **reinvesting into Email & Google Ads**.
  - Resulted in a **15% overall increase in conversion rates** and improved efficiency.

 ## 3. How do you handle conflicting data interpretations when advising clients?
  - When clients interpret data differently, I take a **structured approach** to resolve conflicts:
  - **Understand their perspective**
    - Ask the client **why** they believe a certain interpretation is correct.
    - Identify **assumptions** they are making.
  - **Align on Data Definitions & Metrics**:
    - Ensure both parties use the **same data sources** and metric calculations.
    - E.g. If ROAS differs due to different attribution windows (7-day vs 28-day), align on a consistent window.
  - **Use statistical rigor to settle disputes:
    - Present an **objective statistical analysis** (CIs, p-vals).
    - E.g. If debating whether an ad campaign worked, show the **incremental lift with statistical significance**.
  - **Leverage External Benchmarks or Experiments**:
    - Reference **industry benchmarks** or **Meta's best practices**.
    - If needed, propose a **controlled test** to validate.
  - **Summarize Insights in Business Terms**:
    - Avoid technical jargon. Instead, say:
    - If we increase spend on Fb by 20%, historical data suggests a likely ROI improvement of 10%, but confidence levels indicate some risk. Would you be open to an experiment?

## 4. How would you measure the long-term impact of digital advertising?
- Short-term metrics (CTR, conversions) are easy to measure, but for long-term impact, I would use:
- **Longtidunal Studies & Brand Lift Analysis**:
  - Conduct **survey-based brand lift studies** to measure recall, favorability, and intent over time.
  - Use **time-series analysis** to tract brand mentions and organic searches.
- **Holdout Experiments (Incrementality Testing)**:
  - Select a control group **exposed to no ads** for an extended period. (Hard!)
  - Compare revenue, retention, or LTV after **6-12 months**.
- **Media Mix Modeling (MMM)**:
  - Use **regression models** to isolate the impact of digital ads on long-term outcomes.
  - Account for seasonality, pricing, and macroeconomic factors.
- **Cohort Analysis for Customer LTV**:
  - Segment users who were **acquired via ads vs. organic** and compare:
    - **Retention rates (e.g. 3, 6, 12 months)**
    - **Average revenue per user (ARPU)**.
   
## 5. How would you convince a client to invest in an experimental approach rather than relying on last-click attribution?
- Clients often prefer **last-click attribution** because it's easy to understand, but I'd convince them by:
- **Highlighting the flaws of Last-Click**:
  - Last-click **ignores upper-funnel influence** (e.g., Fb awareness campaigns).
    - Side note: Both Last-Click and First-Click are too simplistic because they:
      - Ignore the full customer journey - Over-credit a single touchpoint and undervalue the impact of others - Fails to capture interactions across multiple touchpoints.
      - Instead, MTA distributes **conversion credit** more fairly across the entire **customer journey**.
  - E.g. A user sees a FB ad but converts via Google search later --> last-click wrongly credits only Google.
- **Show Real Examples where Experiments Work**:
  - Case Study: A **retail client** switched from last-click to **Geo Lift Testing** and dicovered FB ad drove **30% more incremntal sales** than previously thought.
- **Propose a Low-Risk Pilot Test**:
  - Suggest **A/B or incrementality tests** with a **small budget** to demonstrate value.
  - "Let's allocate 5% of your spend to an experiment, and if the results prove valuable, we can scale".
- **Leverage Meta's Own Research & Best Practices**:
  - Meta frequently publishes insights on the benefits of **incrementality testing and MMM**.

## 6. How would you explain p-value and statistical significance to a non-technical stakeholder?
- **In simple terms**, statistical significance means **a result is highly unlikely to have occurred by chance alone, suggesting a real effect or relationship is present, rather than just random variation.
- Also, consider **an analogy**:
  - Imagine flipping a coin 100 times to test if it's fair. If we get 60 Hs, is it luck, or is the coin actually biased?
  - A p-value of 0.03 means there's only a 3% change that this outcome happened by luck.
  - If p-value < 0.05, we can be fairly confident the coin is biased.
- Another analogy for marketing:
  - If we run an A/B Test on an ad campaign and the p-value is 0.02, there's a 2% probability the results are random - so we can be reasonably confident the campaign improved conversions.  

## What is a t-test. Why and when to use it?
* In data analysis, we often compare **2 groups** to see if one performs better than the other. However, just because one group's mean is higher doesn't mean the difference is statistically significant - it could be due to random variation --> Hence, a t-test determine whether the difference is large enough to be consider meaningful.
* Steps: State hypotheses -> Calculate T-statistic -> Compare against critical value or p-value.
* Types of t-Tests and When to Use Them
| **t-Test Type**            | **When to Use**                            | **Example** |
|----------------------------|--------------------------------------------|------------|
| **Independent (Unpaired) T-Test** | Compare two separate groups             | Comparing conversion rates for two ad versions |
| **Paired T-Test**         | Compare before-after or matched pairs      | Measuring sales before vs. after running a Meta Ads campaign |
| **One-Sample T-Test**     | Compare one group against a fixed value    | Checking if email open rates are higher than 20% |
* Key assumptions of a t-test:
  * Data should be normally distributed (for small samples, otherwise CLT applies).
  * Variance between groups should be equal (can be check using Levene's test).
  * The observations should be independent (no repeated measures unless using a paired t-test).
* When NOT to use a t-test:
  * More than 2 groups? Use ANOVA instead.
  * Non-normal data with small samples? Use a Mann-Whitney U Test.
  * Dependent variables? Use a paired t-test or regression analysis. 
* When a lot of assumptions are violated? Use **bootstrapping** - it doesn't rely on strong assumption.

## Explain the following in simple terms: Central Limit Theorem, The Law of Large Numbers
* **CLT**:
  * Statements: 
    * If you take MANY random samples from any population, their average (mean) will form a normal distribution, regardless of the original population’s shape.
    * As the sample size increases, the mean of these samples will get closer to the true population mean.
  * Why is CLT important?
    * It allows us to make inference about a population from a sample.
    * It justifies the use of many statistical methods/models: t-tests, confidence interval, regression models.
    * It works even when the original data is not normally distributed.
      * This is why t-tests (which assume normality) can work **even when our data is skewed**, as long as we have **enough samples**.  (usually, n>=30 is enough). If n is smaller, we need to check if the original data is approximately normal.

## An advertiser (a soap brand) ask to to advise on whether to run ads for a small subset of users (e.g., mom in HCM) versus for all users (all users in Vn). What would you do?

## Overview of Ad Measurement on Mobile Apps
* **1. Key Points of Mobile App Ad Measurement** focuses on tracking **ad performance, user engagement, and conversions** while maintaining user privacy. It typically involves: 
  * **Attribution Models**: assigning credit to the correct marketing channels (e.g., last-click, multi-touch).
  * **Key Metrics**: Installs, clicks, impressions, cost-per-install (CPI), retention, LTV, ROAS.
  * **Tracking Methods**: Mobile Measurement Partners (MMPs), SDK integrations, and device identifiers (e.g., IDFA, GAID).
  * **Privacy Challenges**: Shift towards **privacy-preserving measurement** (e.g., SKAdNetwork, Privacy Sandbox).
  * **Fraud Prevention**: Techniques to detect bot activity, click injection, and fake installs. 
* **2. Key Challenges in Mobile Ad Measurement**
  * It has become more complex due to privacy changes and technical limitations. The main challenges include: 
  * **A. Privacy & Tracking Limitations**
    * **Deprecation of IDFA & GAID** -> Apple's **App Tracking Transparency (ATT)** and Google's **Privacy Sanbox** limit user tracking.
    * **SKAdNetwork (SKAN) * Aggregation** -> Apple's privacy-friendly attribution model provides **limited data** (no user-level tracking).
    * **Google's Privacy Sandbox for Android** -> Moving towards aggregated measurement with **Topics API** and **FLEDGE**.  
  * **B. Attribution & Multi-Touch Complexity**
    * **Last-click attribution is flawed** -> Overestimates the importance of the final touchpoint.
    * **Cross-device & cross-platform tracking is difficult** -> A user might lick an ad on mobile but convert on desktop.
    * **Limited view-through attribution (VTA) data** -> Hard to measure the effect of non-click interactions.
  * **C. Fraud & Data Accuracy Issues**
    * **Ad fraud (e.g., click injection, SDK spoofing, bot installs)** distorts performance metrics.
    * **Self-attributing networks (SANs)** like Meta & Goolge control their own attribution models, limiting transparency.
    * **Delayed reporting** (e.g., SKAdnetwork delays data up to 72 hours) affects real-time optimization.
* **3. How to Ensure Accurate Measurement?**
  * To get **accurate & actionable** mobile ad measurement, consider the following: 
  * **A. Use Privacy-Compliant Tracking Methods**
    * Implement **SKAdNetwork (SKAN) for iOS** and **Privacy Sandbox for Android**
    * Use **first-party data & server-to-server tracking** for better attribution.
    * Invest in **incrementality testing (Geo Lift, Conversion Lift)** instead of relying on last-click model. 
  * **B. Improve Attribution & Multi-Touch Measurement**
    * Use **probabilistic modeling & data-driven attribution** (e.g., **Shapley Value, Markov Chain)**.
    * Implement **unified measurement** across different ad platforms (e.g., MMM + incrementality tests).
    * Leverage **MMPs (AppsFlyer, Adjust, Branch, Singular)** for improved tracking. 
  * **C. Combat Ad Fraud & Data Quality Issues**
    * Use **fraud detection tools** (e.g., AppsFlyer Protect360, Adjust Fraud Prevention).
    * Monitor **post-install engagement** to detect fake installs (e.g., **retention rate drops)**.
    * Set up **real-time anomaly detection** to spot suspicious click & install patterns.
* **4. Privacy & Compliance Considerations**
  * **GDPR & CCPA Compliance** -> Users must **opt-in** to data tracking.
  * **Consent Management Platforms (CMPs)** -> Collect user permissions transparently.
  * **Privacy-Preserving Measurement** -> Adopt **aggregated reporting, differential privacy**, and **synthetic data** techniques. 
* **5. Summary: Future of Mobile Ad Measurement**
* The industry is shiting towards **privacy-first, aggregated, and probabilistic models.**
* Advertisers need to **adapt to SKAN, Privacy Sandbox, and first-party data strategies.**
* **AI-driven attribution & MMM (Marketing Mix Modeling) will become more important** for decision-making.
 
