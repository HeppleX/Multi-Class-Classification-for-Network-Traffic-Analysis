# Multi-Class Classification for Network Traffic Analysis

## Overview

Network traffic analysis is crucial for cybersecurity, enabling timely detection and response to diverse cyber threats. Unlike traditional binary classification methods, this project employs multi-class classification to differentiate between various types of network attacks, including DoS, exploits, reconnaissance, and worms. Utilizing the UNSW-NB15 and CIC UNSW-NB15 augmented datasets, the objective is to enhance cybersecurity threat detection through accurate, nuanced traffic classification.

## Datasets

* **UNSW-NB15 Dataset**

  * [UNSW Research Link](https://research.unsw.edu.au/projects/unsw-nb15-dataset)
  * 257,673 samples
  * 10 classes (1 normal, 9 attack types)

* **CIC UNSW-NB15 Augmented Dataset**

  * [CIC Link](https://www.unb.ca/cic/datasets/cic-unsw-nb15.html)
  * 447,915 samples
  * 10 classes (1 normal, 9 attack types)

## Data Pre-processing

* Retained only numeric features
* Encoded target variable (0-9)
* Removed constant-valued features
* Checked for missing values (none detected)
* Train/test split applied
* Feature selection performed:

  * ANOVA F-test (p-value < 0.05)
  * Pearson correlation (|ρ| ≥ 0.10)

## Models Implemented

1. **Logistic Regression**

   * Pipeline creation for scaling and logistic regression training

2. **Random Forest**

   * 500 trees
   * Balanced class weights
   * Fixed random state for reproducibility

3. **XGBoost** *(Best-performing model)*

   * Gradient-boosted trees optimized for multi-class log-loss
   * Softmax probabilities for output classes

4. **Neural Network**

   * Multiple activation layers
   * ReLU activation and Adam optimizer
   * Batch normalization applied

## Evaluation Results

| Dataset                     | Model               | Accuracy   | Recall | Precision | Macro F1 | Weighted F1 |
| --------------------------- | ------------------- | ---------- | ------ | --------- | -------- | ----------- |
| **UNSW-NB15**               | Logistic Regression | 0.6299     | 0.3141 | 0.3572    | 0.3146   | 0.6476      |
|                             | Random Forest       | 0.7453     | 0.5178 | 0.4897    | 0.4871   | **0.7766**      |
|                             | XGBoost             | 0.7639     | 0.5216 | **0.4980**    | **0.4885**   | 0.7747      |
|                             | Neural Network      | **0.7652** | **0.5562** | 0.4416    | 0.4308   | 0.7617      |
| **CIC UNSW-NB15 Augmented** | Logistic Regression | 0.8937     | 0.3496 | 0.3048    | 0.2979   | 0.8918      |
|                             | Random Forest       | 0.9316     | 0.6760 | **0.5778**    | **0.6137**   | 0.9312      |
|                             | XGBoost             | **0.9364** | **0.7057** | 0.5666    | 0.6099   | **0.9361**      |
|                             | Neural Network      | 0.9303     | 0.6555 | 0.5199    | 0.5446   | 0.9299      |

### Key Observations:

* **XGBoost** provided the highest accuracy and balanced performance across both datasets due to its ability to capture non-linear feature interactions effectively.
* CIC UNSW-NB15 Augmented dataset yielded better performance due to a larger dataset size, better class balance, and augmented features.
* Metrics like recall, precision, and macro F1-score were lower due to class imbalance and the complexity of distinguishing different attack types.

## Future Work

* **Parameter Tuning**: Implement cross-validation to further optimize hyperparameters for each model.
* **Cross-Dataset Transfer Learning**: Explore generalization capabilities across datasets by pre-training models on UNSW-NB15 and fine-tuning on CIC UNSW-NB15 Augmented dataset.
