# Trufflow 1B — Data Product Insight Recommendation

## Summary
- **Task 1 (Insight Detection, NB)**: strong PR-AUC and F1 on weak labels; threshold tuned by F1.
- **Task 2 (Service Similarity)**: cosine NN and KMeans; high silhouette with compact role vectors.
- **Watchlist**: ranked by anomaly impact × cost; includes latest month KPIs.

Artifacts: `task1_results_variants.csv`, `task1_top_incidents.csv`, `task2_neighbors.csv`, `task2_clustering_results.csv`, `watchlist_apps.csv`.

## Task 1 — Insight Detection (Naive Bayes Variants)

| Feature Set / Variant | Precision | Recall | F1 | PR-AUC | Accuracy (+ve) | Accuracy (mean) | Threshold | Valid size | Pos rate (valid) |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Counts only (NB) | 0.10568402532383772 | 0.8179001721170396 | 0.1830056388612474 | 0.1021308496893949 | 0.9179575444635686 | 0.3043420390540036 | 0.3514217132994965 | 308035 | 0.0848767185547097 |
| All features (NB) | 0.9028533849694933 | 0.9451902849493211 | 0.9235196292766784 | 0.9774733165108653 | 0.9451902849493211 | 0.9867125488986641 | 0.9806067807015026 | 308035 | 0.0848767185547097 |
| PCA(3) + NB | 0.6810904129423886 | 0.9355517307324537 | 0.7882821186290465 | 0.6950759672884285 | 0.9355517307324537 | 0.9573457561640722 | 0.154903618666408 | 308035 | 0.0848767185547097 |

## Task 2 — Service Similarity (Top-5 Neighbors, sample)

| service | n1 | s1 | n2 | s2 | n3 | s3 | n4 | s4 | n5 | s5 |
|---|---|---:|---|---:|---|---:|---|---:|---|---:|
| ABTEST | NOTIFY | 0.9999999999809024 | MKTDB | 0.9999999999349333 | DYNPRC | 0.9999999998786389 | XCHATTR | 0.9999999997867001 | TAXCALC | 0.9999999996770227 |
| AIRFLW | HMFRP | 0.999999998609385 | YELLOWS | 0.9999999953721767 | KAFKA | 0.9999999888122127 | DDSD | 0.9999999793005887 | ELASTIC | 0.9999996950612356 |
| ANALAPI | AUTOML | 0.9999992614814076 | RISKMG | 0.9999991143549807 | BILLING | 0.9999989627174771 | GLOBCMP | 0.9999989224119094 | SUPCHN | 0.9999988448202543 |
| APIGWY | SNAPINT | 0.9999999992863867 | MULTILNG | 0.9999999971777137 | SLSDB | 0.9999999962098263 | TAXCALC | 0.9999999958172383 | XCHATTR | 0.9999999955270946 |
| ATLAS | DATAHUB | 0.9999896440875172 | MDLREG | 0.9999718818442569 | JPNXPP | 0.999951212040954 | SPARK | 0.9999474668239722 | PANDRA | 0.9999318254451391 |
| AUTOML | RISKMG | 0.9999999930268135 | BILLING | 0.9999999744404572 | GLOBCMP | 0.9999999675906348 | SUPCHN | 0.9999999532220397 | PAYPROC | 0.9999998582373713 |
| AWS | AZURE | 0.9999999999941895 | SNWFLK | 0.9999999999270122 | DBRCKS | 0.9999999998043644 | HMFRP | 0.7071067811150845 | AIRFLW | 0.7071067796016148 |
| AZURE | AWS | 0.9999999999941895 | SNWFLK | 0.9999999999622053 | DBRCKS | 0.9999999998659184 | HMFRP | 0.7071067811452451 | AIRFLW | 0.7071067797588978 |
| BILLING | GLOBCMP | 0.999999999573766 | SUPCHN | 0.9999999968161862 | RISKMG | 0.9999999940065972 | AUTOML | 0.9999999744404572 | PAYPROC | 0.9999999528774104 |
| CHURNP | FINPLAN | 0.9999999791190787 | INVOPT | 0.9999998271869271 | RTDASH | 0.9999997446540816 | GEOANL | 0.9999995496414685 | TRNPIPE | 0.9999972450839603 |

## Task 2 — Clustering Summary (Silhouette, cosine)

| Representation | Method | k | Silhouette |
|---|---|---:|---:|
| Role means (8-dim) | KMeans | 3 | 0.851158675092405 |
| Role means (8-dim) | KMeans | 4 | 0.8687091680037328 |
| Role means (8-dim) | KMeans | 5 | 0.933113627229332 |
| Role means (8-dim) | KMeans | 6 | 0.9661969420545483 |
| Role means (8-dim) | KMeans | 7 | 0.9631850236343544 |
| Role means (8-dim) | KMeans | 8 | 0.9834557457986388 |
| Role means (8-dim) | KMeans | 9 | 0.9743887732550746 |
| Role means (8-dim) | KMeans | 10 | 0.9673060323981396 |

## Watchlist — Top 20 Apps (by anomaly impact × cost)

| app_id | anomalies_total | score_total | latest_month | cost_latest | cost_mom_pct | value_per_cost_latest | outage_count_latest | outage_duration_latest |
|---|---:|---:|---|---:|---:|---:|---:|---:|
| MCSCBT | 6079 | 4874486.864175227 | 2025-05 | 1522083.049999968 | 0.07695582850548877 | 0.015829359639738805 | 83.0 | 13955.0 |
| CLVMDL | 6695 | 2517525.949247034 | 2025-05 | 1249448.799999955 | 0.06576045593726959 | 0.01809545937376611 | 287.0 | 85770.0 |
| CSTSEG | 3332 | 1580676.073331607 | 2025-05 | 849081.7000000023 | 0.06634769737528308 | 0.014266824971024585 | 1571.0 | 239785.0 |
| SELENE | 0 | 1402166.6285491423 | 2025-05 | 4452273.550000766 | 0.04600896213907379 | 0.029246720476098772 | 2.0 | 205.0 |
| CUSTPRT | 2398 | 1370124.0668129628 | 2025-05 | 708209.9499999983 | 0.10269449470147067 | 0.0 | 16.0 | 1505.0 |
| MOBAPP | 2332 | 1359245.272597053 | 2025-05 | 839258.6499999962 | 0.1474099290780082 | 0.0 | 94.0 | 7320.0 |
| NXPCR | 1662 | 1303846.2622841615 | 2025-05 | 709015.0499999976 | 0.09823546427537842 | 0.017724800058898628 | 68.0 | 9765.0 |
| ECOMLP | 1525 | 1188310.9207149453 | 2025-05 | 760425.2499999962 | 0.0675479634819133 | 0.0 | 3.0 | 395.0 |
| MLOPS | 2792 | 1061194.7956829409 | 2025-05 | 456126.49999999924 | 0.08050451725798735 | 0.0 | 0.0 | 0.0 |
| FEATSTR | 3021 | 944105.7506021918 | 2025-05 | 374757.45000000106 | 0.028273741744478362 | 0.01912917274893397 | 0.0 | 0.0 |
| MDLREG | 2048 | 874775.359788008 | 2025-05 | 211737.15000000008 | 0.08495300472079358 | 0.014795466926800512 | 0.0 | 0.0 |
| FRDETCT | 2092 | 656934.1482520895 | 2025-05 | 386983.35000000143 | 0.05374436396099682 | 0.015206855798834696 | 0.0 | 0.0 |
| WHLSLP | 1381 | 535308.9076280101 | 2025-05 | 339146.30000000127 | 0.0751762972318719 | 0.0 | 1.0 | 105.0 |
| ANALAPI | 1152 | 487097.38598789455 | 2025-05 | 272136.2499999995 | -0.0022670561743084114 | 0.0 | 0.0 | 0.0 |
| CSSRVS | 1191 | 479200.171409473 | 2025-05 | 313706.8 | 0.06056822167660133 | 0.0 | 5.0 | 745.0 |
| ATLAS | 1133 | 463280.72798512795 | 2025-05 | 130588.04999999999 | 0.0778584640679576 | 0.014645291050750808 | 0.0 | 0.0 |
| AUTOML | 1007 | 337040.07735960546 | 2025-05 | 225129.20000000007 | 0.011315970992339695 | 0.0 | 0.0 | 0.0 |
| PAYPROC | 1053 | 333109.37281142065 | 2025-05 | 201876.75000000058 | 0.02852249661705048 | 0.0 | 0.0 | 0.0 |
| RISKMG | 1039 | 325079.8770524587 | 2025-05 | 227378.4999999995 | 0.0796059113300464 | 0.0 | 0.0 | 0.0 |
| TRNPIPE | 708 | 322876.73910406034 | 2025-05 | 233815.1500000005 | 0.06500699406449804 | 0.006814357410116483 | 0.0 | 0.0 |

## Top Incidents — Brief Summaries (sample)

# Top Incidents — Brief Summaries

## 2025-05-12 02:00:00 — ECOMLP → MCSCBT
- **Anomaly score**: p=1.000 (confidence: high), predicted=1, weak_label=1
- **Impact**: req=6, cost_sum=$3,539.95, cost/tx=589.99, data_sum=70.80, data/tx=11.80
- **Signals**: cost/tx high (z=14.7), data/tx high (z=8.2)
- **Next checks**: verify recent deployments/config for `MCSCBT`, inspect capacity/quotas, correlate with upstream `ECOMLP` traffic and provider billing.

## 2025-03-30 01:00:00 — CUSTPRT → MCSCBT
- **Anomaly score**: p=1.000 (confidence: high), predicted=1, weak_label=1
- **Impact**: req=6, cost_sum=$3,465.25, cost/tx=577.54, data_sum=73.05, data/tx=12.18
- **Signals**: cost/tx high (z=14.4), data/tx high (z=8.4)
- **Next checks**: verify recent deployments/config for `MCSCBT`, inspect capacity/quotas, correlate with upstream `CUSTPRT` traffic and provider billing.

## 2025-03-25 05:00:00 — ECOMLP → MCSCBT
- **Anomaly score**: p=1.000 (confidence: high), predicted=1, weak_label=1
- **Impact**: req=5, cost_sum=$2,921.60, cost/tx=584.32, data_sum=59.25, data/tx=11.85
- **Signals**: cost/tx high (z=14.6), data/tx high (z=8.2)
- **Next checks**: verify recent deployments/config for `MCSCBT`, inspect capacity/quotas, correlate with upstream `ECOMLP` traffic and provider billing.

## 2025-04-08 18:00:00 — CUSTPRT → MCSCBT
- **Anomaly score**: p=1.000 (confidence: high), predicted=1, weak_label=1
- **Impact**: req=5, cost_sum=$2,888.40, cost/tx=577.68, data_sum=61.50, data/tx=12.30
- **Signals**: cost/tx high (z=14.4), data/tx high (z=8.5)
- **Next checks**: verify recent deployments/config for `MCSCBT`, inspect capacity/quotas, correlate with upstream `CUSTPRT` traffic and provider billing.

## 2025-05-07 10:00:00 — MOBAPP → MCSCBT
- **Anomaly score**: p=1.000 (confidence: high), predicted=1, weak_label=1
- **Impact**: req=5, cost_sum=$2,884.25, cost/tx=576.85, data_sum=59.85, data/tx=11.97
- **Signals**: cost/tx high (z=14.4), data/tx high (z=8.3)
- **Next checks**: verify recent deployments/config for `MCSCBT`, inspect capacity/quotas, correlate with upstream `MOBAPP` traffic and provider billing.

## 2025-05-13 15:00:00 — MOBAPP → MCSCBT
- **Anomaly score**: p=1.000 (confidence: high), predicted=1, weak_label=1
- **Impact**: req=5, cost_sum=$2,822.00, cost/tx=564.40, data_sum=57.90, data/tx=11.58
- **Signals**: cost/tx high (z=14.1), data/tx high (z=8.0)
- **Next checks**: verify recent deployments/config for `MCSCBT`, inspect capacity/quotas, correlate with upstream `MOBAPP` traffic and provider billing.

## 2025-04-04 18:00:00 — MOBAPP → MCSCBT
- **Anomaly score**: p=1.000 (confidence: high), predicted=1, weak_label=1

_See full: `task1_incident_summaries.md`_