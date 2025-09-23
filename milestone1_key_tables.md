# Key Results — Milestone 1

## Transactions — Coverage
| Item | Value |
|---|---:|
| Transactions rows read | **7,254,656** |
| Aggregated hourly windows | **1,540,175** |
| Feature matrix shape | **(1,540,175, 6)** |

## Data & Feature Engineering (Daily/Monthly)
| Item | Value |
|---|---:|
| Unique services represented | **87** |
| Daily metrics rows / days | **666,855 / 365** |
| Monthly metrics rows / months | **18,270 / 10** |

## Task 1 — Naive Bayes (baseline + variants)
| Feature Set / Variant | Precision | Recall | F1 | PR-AUC | Accuracy (mean) | Threshold | Valid size | Pos rate (valid) |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Counts only (NB) | 0.1057 | 0.8179 | 0.183 | 0.1021 | 0.3043 | 0.3514 | 308,035 | 0.0849 |
| All features (NB) | 0.9029 | 0.9452 | 0.9235 | 0.9775 | 0.9867 | 0.9806 | 308,035 | 0.0849 |
| PCA(3) + NB | 0.6811 | 0.9356 | 0.7883 | 0.6951 | 0.9573 | 0.1549 | 308,035 | 0.0849 |

## Task 1 — PR/Threshold & Confusion (at best-F1 threshold)
| Metric | Value |
|---|---:|
| Best threshold (by F1) | **0.9806** |
| Average precision (PR-AUC) | **0.9775** |
| Accuracy (mean) | **0.9867** |
| Precision / Recall | **0.9028 / 0.9452** |
| F1 | **0.9235** |
| Validation positive rate | **0.0849** |
| Predicted positive rate | **0.0889** |
| Confusion matrix (valid) | **TN=279,230  FP=2,660  FN=1,433  TP=24,712** |

## Task 1 — Top Incidents (from transactions, Top 10)
| time_bucket | consumer_id | supplier_id | probability | predicted_anomaly | weak_label | req_count | error_rate | cost_sum | cost_mean | data_sum | data_mean |
|---|---|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| 2025-05-12 02:00:00 | ECOMLP | MCSCBT | 1 | 1 | 1 | 6 | 0 | 3,539.95 | 589.99 | 70.8 | 11.8 |
| 2025-03-30 01:00:00 | CUSTPRT | MCSCBT | 1 | 1 | 1 | 6 | 0 | 3,465.25 | 577.54 | 73.05 | 12.18 |
| 2025-03-25 05:00:00 | ECOMLP | MCSCBT | 1 | 1 | 1 | 5 | 0 | 2,921.6 | 584.32 | 59.25 | 11.85 |
| 2025-04-08 18:00:00 | CUSTPRT | MCSCBT | 1 | 1 | 1 | 5 | 0 | 2,888.4 | 577.68 | 61.5 | 12.3 |
| 2025-05-07 10:00:00 | MOBAPP | MCSCBT | 1 | 1 | 1 | 5 | 0 | 2,884.25 | 576.85 | 59.85 | 11.97 |
| 2025-05-13 15:00:00 | MOBAPP | MCSCBT | 1 | 1 | 1 | 5 | 0 | 2,822 | 564.4 | 57.9 | 11.58 |
| 2025-04-04 18:00:00 | MOBAPP | MCSCBT | 1 | 1 | 1 | 5 | 0 | 2,768.05 | 553.61 | 61.35 | 12.27 |
| 2025-03-26 21:00:00 | MOBAPP | MCSCBT | 1 | 1 | 1 | 5 | 0 | 2,763.9 | 552.78 | 61.95 | 12.39 |
| 2025-04-03 16:00:00 | ECOMLP | MCSCBT | 1 | 1 | 1 | 5 | 0 | 2,755.6 | 551.12 | 58.5 | 11.7 |
| 2025-04-07 23:00:00 | ECOMLP | MCSCBT | 1 | 1 | 1 | 5 | 0 | 2,743.15 | 548.63 | 59.4 | 11.88 |

## Task 2 — Service Similarity & Clustering (Cosine)
| Item | Value |
|---|---:|
| Services (vectors) | **87** |
| Role vector dimensionality | **8** |
| Best k (KMeans, cosine) | **8** |
| Silhouette (cosine) @ best k | **0.9835** |

### Clustering Sweep (Silhouette over k)
| k | Silhouette (cosine) |
|---:|---:|
| 3 | 0.8512 |
| 4 | 0.8687 |
| 5 | 0.9331 |
| 6 | 0.9662 |
| 7 | 0.9632 |
| 8 | 0.9835 |
| 9 | 0.9744 |
| 10 | 0.9673 |

### Nearest Neighbors (Top-5 per service, sample of 15)
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
| CLVMDL | FRDETCT | 0.9999867575340989 | JPCHRN | 0.9999861324591605 | CSTSEG | 0.9999657701919727 | NXPCR | 0.9996663214715518 | FINPLAN | 0.9983495941850906 |
| COHORT | MDLMON | 0.9999999997091353 | EXPENSE | 0.9999999993846884 | ECOMLP | 0.9999999988430851 | HRANAL | 0.9999999985478576 | MOBAPP | 0.9999999948105134 |
| COMPLT | YGSCST | 0.9993169545279368 | SELENE | 0.9993059929680114 | FEATSTR | 0.9993050391297625 | YGCHRN | 0.9992906248234389 | YGCLV | 0.9992629508681211 |
| CSSRVS | WHLSLP | 0.9999999999955765 | JRNYANL | 0.9999999999943455 | TEMPANL | 0.9999999998982382 | DEMAND | 0.9999999997698144 | DATARES | 0.9999999994512166 |
| CSTSEG | JPCHRN | 0.9999950283282881 | FRDETCT | 0.9999912877150843 | CLVMDL | 0.9999657701919727 | NXPCR | 0.999845795314919 | FINPLAN | 0.99879030604854 |

## Watchlist — Top 5 Apps by Anomaly Impact × Cost (validation slice)
| # | App | Anomalies (total) | Score_total | Latest month | Cost_latest | MoM cost % | Value/Cost (latest) | Outages (count / duration) |
|---:|---|---:|---:|---|---:|---:|---:|---:|
| 1 | MCSCBT | 6,079 | 4,874,486.86 | 2025-05 | 1,522,083.05 | 0.077 | 0.01583 | 83 / 13,955 |
| 2 | CLVMDL | 6,695 | 2,517,525.95 | 2025-05 | 1,249,448.8 | 0.0658 | 0.0181 | 287 / 85,770 |
| 3 | CSTSEG | 3,332 | 1,580,676.07 | 2025-05 | 849,081.7 | 0.0663 | 0.01427 | 1,571 / 239,785 |
| 4 | SELENE | 0 | 1,402,166.63 | 2025-05 | 4,452,273.55 | 0.046 | 0.02925 | 2 / 205 |
| 5 | CUSTPRT | 2,398 | 1,370,124.07 | 2025-05 | 708,209.95 | 0.1027 | 0 | 16 / 1,505 |
