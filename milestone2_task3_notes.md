# Milestone 2 — Task 3: Feature Refinement (quick sweep)

We tuned **KNN (k ∈ {3..15 odd})** and **Logistic Regression (C ∈ {0.1..10})** on the **Top-3** feature set ([req_count, cost_sum, cost_mean]) using the same time-based validation split.

- **Best so far:** KNN_k=15 — F1=0.9943, PR-AUC=0.9925, Acc=0.9990, Prec=1.0000, Rec=0.9887, Thr=0.3987
- See `task3_feature_refinement_results.csv` for the full sweep.

_Next: lock in the best config for Task 4 docs, and (optionally) try small tweaks (e.g., KNN leaf_size, LogReg class_weight=None vs 'balanced')._