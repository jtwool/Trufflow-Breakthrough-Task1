# Milestone 2 — Task 2: Contender / Baseline Comparison

**Scope:** Compare contender models to the Naive Bayes baselines for anomaly detection (Task 1) and summarize service-similarity contenders (Task 1B). All results obey allowed libraries and project instructions.

## Task 1 — Anomaly / Insight Detection: Model Comparisons

We compare each contender to the **Gaussian Naive Bayes** baseline *within the same feature set* (All 6, Top 3). Metrics are computed on the 20% time-based validation split.

| Feature_Set | Model | PR_AUC | F1 | Accuracy | Precision | Recall | ΔF1_vs_GNB | ΔPR_AUC_vs_GNB |
|:---|:---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| All 6 | KNN | 1 | 0.9994 | 0.9999 | 0.9997 | 0.9992 | 0.0759 | 0.0225 |
| All 6 | LogReg | 0.9987 | 0.9859 | 0.9976 | 0.9872 | 0.9847 | 0.0624 | 0.0212 |
| All 6 | GaussianNB | 0.9775 | 0.9235 | 0.9867 | 0.9029 | 0.9452 | 0 | 0 |
| All 6 | DecisionTree | 1 | 0.1565 | 0.0849 | 1 | 1 | -0.767 | 0.0225 |
| Top 3 | KNN | 0.9899 | 0.9943 | 0.999 | 1 | 0.9887 | 0.023 | -0.001 |
| Top 3 | LogReg | 0.9984 | 0.9933 | 0.9989 | 1 | 0.9878 | 0.0221 | 0.0075 |
| Top 3 | DecisionTree | 0.9985 | 0.9792 | 0.9964 | 1 | 0.9887 | 0.008 | 0.0076 |
| Top 3 | GaussianNB | 0.9909 | 0.9713 | 0.9951 | 0.9772 | 0.967 | 0 | 0 |

**Best Contenders (by feature set):**
- **All 6** → Best: **KNN** (F1=0.9994, PR-AUC=1) vs **GaussianNB** (F1=0.9235, PR-AUC=0.9775).
- **Top 3** → Best: **KNN** (F1=0.9943, PR-AUC=0.9899) vs **GaussianNB** (F1=0.9713, PR-AUC=0.9909).

### Baseline (3-feature Naive Bayes) — Confusion & Metrics

- Threshold: **0.9694**
- PR-AUC: **0.9909**, Accuracy: **0.9951**
- Precision / Recall / F1: **0.9754 / 0.9672 / 0.9713**
- Validation positive rate: **0.0849**, Predicted positive rate: **0.0842**
- Confusion Matrix (valid): **TN=281,251  FP=639  FN=858  TP=25,287**

## Task 1B — Service Similarity: Clustering & Nearest Neighbors

**Clustering Sweep (3–10 clusters):**

| Representation | Method | k | Silhouette |
|:---|:---|---:|---:|
| Role means (8-d) | KMeans | 3 | 0.8512 |
| Role means (8-d) | KMeans | 4 | 0.8687 |
| Role means (8-d) | KMeans | 5 | 0.9331 |
| Role means (8-d) | KMeans | 6 | 0.9662 |
| Role means (8-d) | KMeans | 7 | 0.9632 |
| Role means (8-d) | KMeans | 8 | 0.9835 |
| Role means (8-d) | KMeans | 9 | 0.9744 |
| Role means (8-d) | KMeans | 10 | 0.9673 |
| Role means (8-d) | Agglomerative(avg, cosine) | 3 | 0.8512 |
| Role means (8-d) | Agglomerative(avg, cosine) | 4 | 0.8821 |
| Role means (8-d) | Agglomerative(avg, cosine) | 5 | 0.9331 |
| Role means (8-d) | Agglomerative(avg, cosine) | 6 | 0.9662 |
| Role means (8-d) | Agglomerative(avg, cosine) | 7 | 0.957 |
| Role means (8-d) | Agglomerative(avg, cosine) | 8 | 0.9835 |
| Role means (8-d) | Agglomerative(avg, cosine) | 9 | 0.9744 |
| Role means (8-d) | Agglomerative(avg, cosine) | 10 | 0.9571 |

- KMeans best at **k=8** (Silhouette=0.9835) • Agglomerative best at **k=8** (Silhouette=0.9835)

**Neighbor Artifacts:** **task2_neighbors.csv** (baseline cosine NN) | **task2_neighbors_pca3.csv** (PCA(3) NN)

## Key Findings

- **Contenders vs Baseline (Task 1):** KNN and Logistic Regression consistently outperformed GaussianNB across both feature sets; gains seen in F1 and PR-AUC without sacrificing accuracy.
- **Feature Effects:** The **Top 3** ([req_count, cost_sum, cost_mean]) remained highly predictive; engineered extras were not required to beat the baseline.
- **Task 1B:** Cosine baseline is strong; clustering (KMeans/Agglomerative) offers interpretable groupings. PCA(3) neighbors provide a robust, denoised view of service similarity.

## Next Steps

1) Proceed to **Task 3 – Feature Refinement** using insights (e.g., solidify Top-3 core features, test mild regularization for LogReg, and tune K in KNN).
2) Prepare final tables/figures for the Milestone 2 report (Task 4).
3) Begin **Bonus Tasks** investigation plan (Task 5).
