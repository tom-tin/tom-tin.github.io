---
layout: post
title:  "Overview of Amazon QuickSight"
date:   2025-07-02 10:00:00 +0700
categories: [cloud, aws, viz]
---

### Introduction
* Amazon QuickSight: BI tool. 
* Amazon Q: a genAI-powered dashboard / report-building tool to explore data quickly.
* How QuickSight is different from Amazon Q? 
  * Q is a genAI capability (an separate product) and is integrated with QuickSight that allows user to interact with QS using natual language.
  * In QuickSight --> Security & Permission --> Need to Enable Amazon Q.
  * Need to create a Topic.
    * It's like a context / project to provide to the LLM.
    * Connect to a dataset.
      * Columns have to be meaningful?
  * Questions:
    * Do we need to provide example for Amazon Q to learn first?
    * How to validate the answer provided by Q?
      * E.g. in Databricks Genie, we can also see the underlying SQL query correspond to the English question and then can validate and correct it so that it can do better next time.
      * There is a User Activity section where user can provide feedbacks.
    * What model underneath Q?
      * Use multiple models such as Nova. From tools like Amazon Bedrock.  

### Features
#### Interactive Dashboard
* AI-assisted data storytelling: tell it to generate a report based on dashboard.
* An advanced AI agent.

#### Ad-hoc Analysis
* Users can ask ad-hoc questions (on-demand).

#### Machine Learning
* Anomaly detection.
* Forecasting.
* NLQ (not realy ML)?
* Questions:
  *  

#### Natural Language Querying (NLQ)

#### Embed dashboards into applications

#### Misc
* Fast, in-memory engine called SPICE for efficient query performance. (Super-fast, Parallel, In-memory Calculation Engine)
* RLS
* Paginated Reporting

### Pricing?
* By usage, sessions. Can charged based on roles and number of users in each role.

### Data Source Connectivity
* * AWS: Redshift, S3, RDS.
  * On-prem: databases, SaaS application.

### Compare to other tools
* v.s. Microsoft's PBI, Databricks' Genie: Each integrate better with their own cloud ecosystem.
* QS: UI is not as user-friendly, graph/chart library is less extensive than some rivals.
  * Can't extract underlying SQL like Genie. 
* Databricks' Genie:
  * Limited on dashboard.
* PBI: 

### Reference
