---
layout: post
title:  "Some notes on para/hyper-para of a few ML models"
date:   2025-03-13 14:00:00 +0700
categories: [ml, parameters]
---

## Random Forest
* n_estimators: num of trees (default: 100).
* Below 3 are about setting the minimum impurity decrease in order to split a node.
  * max_depth: max depth of each tree (to prevent overfitting).
  * min_samples_split: minimum samples required to split a node.
  * min_samples_leaf: minimum samples required to be a leaf node.
* max_features: number of features to consider for best split (sqrt for classification, log2 is common).
  * sqrt is just rule of thumb and should be ok. But we should check up to 30-40% of total features.
  * Higher -> can overfit.  
* bootstrap: whether to bootstrap sampling (default: True).
* oob_score: out-of-bag scoring for validation (True/False).
* criterion: splitting criterion ("gini" or "entropy" for classification, "mse" or "mae" for regression).
  * These are different ways to assess how similar/different two samples are.
* seeding: RF also have this to resuse previous training, like GB.
* Side note:
  * Bagging is a general concept where the individual models can be different than trees.
  * Also for bagging, all features are used when splitting a node. For RF, only a fraction (usually improve).
  * RF, GB, SVM are non-parametric models (i.e., complexity grows as the number of training samples increases).
    * RF handles multi-class classification better than SVM, since RF does it out-of-the-box.
  * In theory, RF should work with missing and categorical data. However, the sklearn implementation doesn't handle this. To prepare data for RF, you need to make sure that:
    * there are no missing values in your data
    * convert categorical data into numerical.
  * Usually, XGB is better than RF, maybe giving 2% improvement. But it comes as the cost of MUCH longer (maybe 50 times) training time because it can by nature NOT run in parallel like RF.
  * Note that one drawback for GBT is: In Spark 2.3.0, GBT cannot support multi-class classification yet. But RF can.
 

  ## Gradient Boosting (GB) (GBM, GBT)
  * n_estimators: number of boosting stage (default: 100).
    * Usually choose a high value. But too high can overfit. 
  * learning_rate: shinks contribution of each tree (lower values need more trees).
    * But lower value prevent overfit. 
  * Same as RF: max_depth, min_samples_split, min_samples_leaf.
  * subsample: fraction of samples used per boosting iteration (default: 1.0 i.e. used all).
    * Values slightly <1 such as 0.8 make model robust by reducing variance. 
  * loss: loss func ("deviance" for classification, "ls" for regression).
  * alpha: used in quantile loss for quantile regression.
  * warm_start: whether to reuse previous training results (True/False).
 
  ## XGB (aka, GBM killer, or regularized GB)
  * Key: XGB allows for tree pruning. You can tune the amount of pruning with a parameter eita.
  * 3 key parameters to tune XGB: the learning rate (alpha), the regularization parameter (gamma), and the amount of pruning (eita).
  * XGBoost is currently not available on pyspark 2.4.4.
  * Both xgboost and gbm follows the principle of gradient boosting. There are however, the difference in modeling details. Specifically, xgboost used a more regularized model formalization to control over-fitting, which gives it better performance.
    *  
