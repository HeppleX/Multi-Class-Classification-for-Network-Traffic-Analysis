# Multi-Class-Classification-for-Network-Traffic-Analysis

## 1 · Project Summary
This repository contains a **full, reproducible pipeline** for detecting and categorising malicious network traffic.  
Two well-known intrusion–detection data sets are used:

| Data set | Description |
|----------|---------------------|
| **UNSW-NB15**<br>*(training-set.csv, testing-set.csv)* | Benchmark with 9 attack categories + Benign, already split by the authors. https://research.unsw.edu.au/projects/unsw-nb15-dataset|
| **CIC UNSW-NB15 Augmented**<br>*(Data.csv + Label.csv)* | A richer, flow-statistic version used to test scalability. https://www.unb.ca/cic/datasets/cic-unsw-nb15.html|

The workflow covers loading, cleaning, **feature selection** (ANOVA + correlation), and training / evaluating four classifiers:

* Logistic Regression  
* Random Forest  
* XGBoost  
* Neural Network

A universal helper, `evaluate_model`, prints core metrics (Accuracy, Precision, Recall, F1-Score and F1-score(weighted)) **and** plots confusion matrices + One-vs-Rest ROC curves for every class.

---


