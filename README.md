## Milestone 2 — Summary

**Artifacts**
- `task1_contender_results.csv` — Task 1 baseline + contenders (metrics on time-split validation).
- `task2_neighbors.csv`, `task2_neighbors_pca3.csv` — Service cosine neighbors (raw & PCA(3)).
- `task2_clustering_results.csv` — KMeans & Agglomerative silhouette sweep (k=3..10).
- `task3_feature_refinement_results.csv` — KNN (k sweep) and Logistic Regression (C sweep).
- `milestone2_task2_report.md` — Consolidated comparisons and findings.

**Highlights**
- Top-3 features remain very strong; KNN/LogReg beat GaussianNB on F1 and PR-AUC.
- Service clusters are compact with cosine; best silhouette near k≈8.


## Milestone 2 — Summary
- Task 1: GaussianNB baseline vs contenders (KNN, LogReg, DecisionTree) on All-6 and Top-3 features.
- Task 1B: Cosine neighbors; KMeans/Agglomerative clustering; PCA(3) neighbors.
- Task 3: Refinement sweep — best KNN k≈11–15; LogReg C≈0.1–1.0.
- See `Milestone2_Final_Report.md` and the figures for details.


### Figures (Milestone 2)
- `fig_task1_f1.png` — F1-scores: balance of precision & recall for Task 1 models.
- `fig_task1_prauc.png` — PR-AUC: how well models rank anomalies vs normal.
- `fig_task2_silhouette.png` — Silhouette by k: best cluster separation for services.
