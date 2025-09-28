# Milestone 1 — Features & Selection (Artifacts)

## Feature Snapshot

- `features_snapshot_first10.csv`: first 10 rows with (consumer, supplier, hour) and 6 features.
- `features_summary_stats.csv`: count/mean/std/min/25%/50%/75%/max per feature.

## Feature Audit

- `feature_variance.csv`, `feature_feature_correlation.csv`, `feature_label_correlation.csv`, `feature_mutual_information.csv`.

## Model Selection (Naive Bayes)

- `model_selection_results.csv`: **All 6 vs Reduced 3** features.
- Best (expected): **Reduced 3** — check F1/PR-AUC in the table.
- Also saved: `task1_pr_curve_selected.csv`, `task1_confusion_summary_selected.json`, `task1_top_incidents_selected.csv`.
