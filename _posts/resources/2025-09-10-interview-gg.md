---
layout: post
title:  "Interview Resources - DS GG"
date:   2025-09-01 14:00:00 +0700
categories: [data, resources, interviews, DS]
---

## Strategies
* Focus on structuring your answers clearly, using data-driven insights to support your recommendations.

## Q - Coding

## Q - Open - Business
* Notes:
  * product thinking, data intuition, business acumen, experimentation/design strategy. 
* How would you **measure the success of a new feature** introduced on a Google product?
  * Define the Feature & Objective.
    * Purpose of feature: drive engagement, retention, revenue.
    * Gmail: "smart reply" --> improve user response time, interaciton rate.
    * Chrome: "Tab Grouping" --> allow users to organize tabs.
      * Hypo: helps reduce cognitive load and improves tab/session management. 
  * Identify Success Metrics.
    * Primary metrics (direct impact):
      * Features useage rate (%user using), task success rate (emails replied within X minutes), engagement metrics (session length, email send rate)
    * Secondary metircs: retention rate, NPS/user satisfaction, error rate / user drop-off. 
  * Set a Baseline and Design an Experiment.
    * A/B test if feasible: need sample size, power, metric volatility.
    * Include pre-post analysis and holdout groups if global rollou;t is needed.  
  * Check for Trade-offs (guardrail).
    * Did it negatively impact other features (e.g., cannibalizing other tools).
    * Was latency or load time increased? 
  * Long-term View.
    * Check for user behavior change over time (cohort analysis).
    * Are users becoming dependent, or is novelty fading?
* What strategies would you suggest to **increase customer retention** on a Google service?
  * Define Retention Clearly.
    * Day 1, 7, 30 retention?
    * Based on login, key actions, or revenue-generating behavior? 
  * Identify Causes of Churn.
    * Analyze user behavior pre-churn.
    * Survey or feedback loops.
    * Session frequency, feature drop-off, frustration signals. 
  * Segmentation.
    * Power users vs casual users, old vs new.
    * Geography, device, acquisition channel. 
  * Stategies to Improve Retention
    * Personalization: Tailor onboarding, UI, notifications.
    * Nudges & Reminders: Push/email to re-engage dormant users.
    * Habit-forming features: e.g., streaks, rewards, saved preferences.
    * Performance improvements: faster load time, less friction.
    * Incentive / Gamification. 
  * Measure Impact.
    * A/B test retention strategies.
    * Use survival analysis, cohort retention curves, hazard models. 
* If Google wanted to **improve user engagement** on a platform, what data would you analyze, and what metrics would you use?
  * Define "Engagement" for the Platform.
    * Youtube: watch time, session length.
    * Search: query frequency, CTR, dwell time.
    * Chrome: 
  * Metrics to Analyze.
    * Active users (DAU/WAU/MAU)
    * Session metrics: frequency, duration, depth.
    * Churn / bounce rates.
    * Stickiness (DAU/MAU)
    * Time-to-action: how quickly users perform key actions. 
  * Data Analysis Plan
    * Segmentation: power users vs casual users, new vs returning
    * Funnels: Drop-off at each stage of engagement.
    * Time-series: Look at trends before and after changes.
    * Correlations: What features correlate with high engagement?
  * Hypotheses to Explore
    * Which content types, UI changes, or devices drive more engagement?
    * Do certain referral sources lead to low-engagement users? 
  * Interventions
    * Use the data to design tests (e.g., UI tweaks, nudges, notifications)
    * Personalization / contextual relevance improvements.
    * Analyze lift from changes using incrementality testing. 
* How would you approach **designing a recommendation system** for Google users?
   * Understand Context & Objective.
     * What products? (YouTube, News, Play Store)
     * What is the goal? (Engagement? Discovery? Monetization?) 
   * Type of Recommendation Systems.
     * Content-based filtering (user-item metadata similarity)
     * Collaborative filtering (user-user or item-item matrix factorization)
     * Contextual Bandits / RL (for adaptive recommendations)
     * Hybrid systems (combination of the above) 
   * Data Needed
     * User profiles & history
     * Item metadata (text, tag, categories)
     * Implicit feedback (clicks, watch time) vs explicit (ratings, likes)
     * Contextual signals (location, time, device, recency) 
   * Model Design.
     * Start simple: popularity-based or rule-based.
     * Move to:
       * Matrix Factorization (ALS, SVD)
       * Neural Recommenders (e.g., YouTube DNN architecture)
       * Contextual MAB.
     * Use embeddings to handle user/item similarity.  
   * Metrics.
     * Offline: Precision@K, Recall@K, NDCG, MAP.
     * Online: CTR, watch time, engagement, conversion.
     * Also monitor diversity, serendipity, and fairness. 
   * Experimentation.
     * A/B test recommendation changes carefully.
     * Account for feedback loops, novelty bias, cold-start issues. 


## Q - Stats
* Notes:
  * Use simple terms. Show how you apply them in practice. 
* Given a coin, design an experiment and analyze its result to find out if the coin is biased.
* Explain the difference between Type I and Type II errors. How would you control them in an experiment?
* How would you determine the sample size required for an A/B test at Google?
* What is p-value, and how would you interpret it in the context of an A/B test result?
* Explain the concept of confidence intervals and how they are useful in making business decisions.
* Basic:
 * Given a sample with 100 obs, with sample mean = 100, se = 3. Note that se of that sample mean is: std / sqrt(n) = std / 10.
  * What is se? It's the std of the sampling distribution. Meaning the distribution we get when we repeat the above sampling process.
  * What assumption do we need to get the above se formula? The sample size needs to be large enough so that the CLT applies and hence the sampling distr. is Normal.
  * What is the formula for the se of the sample median? Usually we don't have a close form for that, but we can use boostrap method. I think another answer is in case n is large enough, the sampling distr is Normal hence we have the same sample mean and sample median --> same se as well.
* Experiments:
 * Given 2 approaches on measuring an effect of a drug on human, comment on their strengths/weaknesses.
  * Approach 1: Divide a group of 100 people: group A take the drug, group B take the placebo, measure the effects on both group such as heart rate.
  * Approach 2: Let all 100 ppl take the placebo without telling them. After 2 weeks, let them take the drug and measure the effect.
 * If we were to repeate approach 1 over and over different groups of people, would the effect be still bias? No, as we repeat more and more it is an unbiased estimator.
* Prob:
 * Assume the distribution of children per family is given by: 

| n_children | 0 | 1 | 2 | 3 | 4 | >=5 |
|---|---|---|---|---|---|---|
| p | 0.3 | 0.25 | 0.2 | 0.15 | 0.1 | 0 |

 * Consider a random girl in the population of children. What's the probability that she has a sister?
  * A = event: a random girl has a sister
  * P(A) = P(2sib) * P(A|2sib) + P(3sib) * P(A|3sib) + P(4sib) * P(A|4sib)
  * P(A|2sib) = 1/2, P(A|3sib) = 3/4, P(A|4sib) = 7/8
  * P(2sib) = (0.2*2) / (0.25*1 + 0.2*2 + 0.15*3 + 0.1*4)
  * P(3sib) = (0.15*3) / (0.25*1 + 0.2*2 + 0.15*3 + 0.1*4)
  * P(4sib) = (0.1*4) / (0.25*1 + 0.2*2 + 0.15*3 + 0.1*4) 


## Q - ML
* Notes:
  * Your approach: handling data, feature selection, model building, eval metrics. 
* How would you build a model to predict a user's likelihood of engaging with a Google service?
* Describe a time when you used feature engineering to improve a machine learning model’s performance.
* How do you handle imbalanced datasets in a classification problem?
* Explain the differences between supervised and unsupervised learning with examples relevant to Google.

## Q - Behavioral
* Why are you interested in Google?
* What relevant experience do you bring to this role?
* Can you describe a challenging project where data analysis was central to the outcome?

## Google's Product Metrics

## Google's Mission and Values

## Ref
* [Google Data Scientist Interview](https://www.datainterview.com/blog/google-data-scientist-interview)
