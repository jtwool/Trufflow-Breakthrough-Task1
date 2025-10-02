Project - Data Product Insight Recommendation

Team: Trufflow 1b

We use Trufflow’s structured app-to-app transaction data to (1) detect and prioritize anomalous behavior and (2) map service similarity for consolidation and investigation. Tools used (Milestone 1): Python, NumPy and scikit-learn. Baseline classifier: Naive Bayes. Similarity: cosine (with KMeans for clustering). License: Apache-2.0.

Data

We worked with three .jsonl files:

transactions.jsonl: per-transaction records with consumer/supplier IDs, time, cost, data volume, and response outcome.

daily_metrics.jsonl: per-app daily rollups (cost, value, data, requests...).

monthly_metrics.jsonl: per-app monthly rollups (same, plus outage metrics).

Quick stats

Transactions rows read: 7,254,656

Aggregated hourly windows: 1,540,175

Feature matrix shape: (1,540,175, 6)

Unique services: 87

Daily metrics rows / unique days: 444,570 / 365

Monthly metrics rows / unique months: 18,270 / 10

Milestone 1 - What we built
Task 1 - Insight Detection (Naive Bayes baseline)

Aggregate transactions.jsonl to hourly windows per (consumer, supplier).

Features: req_count, error_rate, cost_sum, cost_mean, data_sum, data_mean.

Weak labels (baseline supervision): mark anomalous if error_rate > 10% OR robust z-score of cost_mean or data_mean > 3.

Time-aware split (80/20 by hour) to avoid leakage.

Train GaussianNB with standardization; choose threshold by max F1 on validation.

Results (All features, Naive Bayes)

PR-AUC: 0.9775

F1: 0.9235

Precision / Recall: 0.9029 / 0.9452

Accuracy (mean): 0.9867

Best-F1 threshold: ~0.9806

Confusion (validation): TN=279,230; FP=2,660; FN=1,433; TP=24,712

Validation positive rate: ~8.49%; Predicted positive rate: ~8.89%

Variants (for comparison)

Feature Set / Variant	Precision	Recall	F1	PR-AUC	Accuracy (Mean)	Threshold	Valid Size
Counts only (NB)	0.1057	0.8179	0.1830	0.1021	0.3043	0.3514	308,035
All features (NB)	0.9029	0.9452	0.9235	0.9775	0.9867	0.9806	308,035
PCA(3) + NB	0.6811	0.9356	0.7883	0.6951	0.9573	0.1549	308,035

Top incidents (examples)

ECOMLP → MCSCBT: p=1.00, cost/tx ~ 589.99, data/tx ~ 11.80

CUSTPRT → MCSCBT: p=1.00, cost/tx ~ 577.54, data/tx ~ 12.18

ECOMLP → MCSCBT: p=1.00, cost/tx ~ 584.32, data/tx ~ 11.85
These are unusually expensive/heavy hours and good places to investigate first.

Feature Selection & Feature Creation (Task 1)

We audited the six inputs to see which ones truly add signal and which ones overlap. Feature-to-feature correlations showed strong redundancy: total cost and total data moved almost one-to-one (corr ≈ 0.91), and average cost and average data did too (corr ≈ 0.91). The error_rate column was nearly constant and contributed very little. Mutual-information scores (higher is better) ranked the inputs as: cost_mean ≈ 0.290, data_mean ≈ 0.175, cost_sum ≈ 0.118, data_sum ≈ 0.074, req_count ≈ 0.021, error_rate ≈ 0.000.
Based on this, we kept three non-redundant features—request count, total cost, and average cost—and retrained the exact same Naive Bayes with the same time split and F1-based thresholding. The simpler model performed better on validation: PR-AUC ≈ 0.9909, Precision/Recall ≈ 0.9772/0.9670, F1 ≈ 0.9713, Accuracy ≈ 0.9951, best threshold ≈ 0.9694; confusion at that threshold: TN=281,251; FP=639; FN=858; TP=25,287.
We also tested engineered features (log transforms of cost/requests, pair-wise “how unusual is this pair right now” z-scores, and hour/day cyclical encodings). On this dataset those extras were slightly worse (PR-AUC ≈ 0.9819, F1 ≈ 0.9377), so for Milestone 1 we adopted the lean 3-feature Naive Bayes as the core model.

Task 2 - Service Similarity (Cosine) and Clustering

We built compact 8-dimensional "role" vectors per service (consumer and supplier behavior averaged, request-weighted), then:

Nearest neighbors via cosine similarity (find look-alike services).

KMeans clustering; quality scored by silhouette (cosine).

Results

Services represented: 87

Best k: 8

Silhouette (cosine) at best k: ~0.9835

Sample nearest neighbors

ABTEST → NOTIFY, MKTDB, DYNPRC, XCHATTR, TAXCALC

AWS ↔ AZURE, SNWFLK, DBRCKS (infra/data platform cluster)

APIGWY → SNAPINT, MULTILNG, SLSDB, TAXCALC, XCHATTR

Used neighbors/clusters to review overlaps and possible consolidations.

Watchlist - What to fix first

We rank apps by anomaly impact (model probability × cost_sum) over the validation slice, then enrich with monthly KPIs (latest month cost, MoM %, value-per-cost, outage counts/duration).

Top 5 by impact

#	App	Anomalies (total)	Score (impact approx)	Latest Month	Cost	MoM %	Value/Cost	Outages (count / duration)
1	MCSCBT	6,079	4,874,486.86	2025-05	1,522,083.05	0.07696	0.01583	83 / 13,955
2	CLVMDL	6,695	2,517,525.95	2025-05	1,249,448.80	0.06576	0.01810	287 / 85,770
3	CSTSEG	3,332	1,580,676.07	2025-05	849,081.70	0.06635	0.01427	1,571 / 239,785
4	SELENE	0	1,402,166.63	2025-05	4,452,273.55	0.04601	0.02925	2 / 205
5	CUSTPRT	2,398	1,370,124.07	2025-05	708,209.95	0.10269	0.00000	16 / 1,505

Keep, Trim and Fix now

Keep (necessary): core paths that carry real traffic reliably at normal cost.

Review for consolidation (might be extra): services in the same similarity cluster doing similar work.

Fix now (needs attention): start with the Watchlist Top-5 above.
Translation: these five deliver the most impact and need to be tackled first.

How to reproduce (Jupyter)

We ran everything in VS Code Jupyter. Each step is a single cell.

Inspect schemas for the three JSONL files.

Aggregate transactions → hourly features (produces X and keys).

Train Task 1 (Naive Bayes) and compute metrics (PR-curve points, confusion).

Task 2: cosine neighbors + KMeans silhouette sweep.

Top incidents & summaries saved to CSV/MD.

Daily/Monthly pivots to CSV.

Watchlist CSV (impact ranking + latest month KPIs).

Report tables combined in report_pack.md (plus milestone1_key_tables.md).

Artifacts already produced:
task1_results_variants.csv; task1_confusion_matrix.csv; task1_confusion_summary.json; task1_pr_curve.csv; task1_top_incidents.csv; task1_incident_summaries.md; task2_neighbors.csv; task2_clustering_results.csv; task2_clusters_k8.csv; daily_features.csv; monthly_features.csv; watchlist_apps.csv; milestone1_key_tables.md; report_pack.md.

Design decisions

Weak supervision: robust outliers and error-rate until ground-truth labels arrive.

Time-aware split: prevents look-ahead leakage; mirrors real deployment.

Cosine similarity on compact role vectors: stable, interpretable grouping.

Impact ranking: converts scores into a clear action list.

Limitations

Weak labels can over/under-flag; when ground truth arrives, we will re-train and calibrate thresholding.

Ratio features can blow up near zero; we add small safety values to avoid divide-by-zero and can add winsorization/caps if needed.

What's next (Milestones 2)

Milestone 2 — Contenders & comparisons (planned)

Task 1: try Logistic Regression, calibrated SVM, small Random Forest/GB vs. NB on multiple feature sets (counts, all, PCA, +time, +KPIs). Report PR-AUC/F1 and a compact markdown table.

Task 2: test alternative representations + clustering (cosine KNN, KMeans, Agglomerative). Report silhouette and a short neighbor/cluster summary.

Bonus (investigate): early-warning label shifts; LLM summary plan + tiny eval rubric.

Milestone 3 — Refine & package (planned)

Pick best models, tune thresholds, and (optionally) execute one bonus (early warning or LLM summaries).

Finalize comparison tables, brief slide deck, and tag a release.

License

Apache-2.0.
