# Milestone 2 — Task 2: Contender vs Baseline Comparison

**Scope:** Compare contender models to the Naive Bayes baselines for anomaly detection (Task 1) and summarize service-similarity contenders (Task 1B).

## Task 1 — Anomaly / Insight Detection: Model Comparisons
| Feature_Set | Model | PR_AUC | F1 | Accuracy | Precision | Recall | ΔF1_vs_GNB | ΔPR_AUC_vs_GNB |
|:---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| All 6 | KNN | 1 | 0.9994 | 0.9999 | 0.9997 | 0.9992 | 0.0759 | 0.0225 |
| All 6 | LogReg | 0.9987 | 0.9859 | 0.9976 | 0.9872 | 0.9847 | 0.0624 | 0.0212 |
| All 6 | GaussianNB | 0.9775 | 0.9235 | 0.9867 | 0.9029 | 0.9452 | 0 | 0 |
| All 6 | DecisionTree | 1 | 0.1565 | 0.0849 | 1 | 1 | -0.767 | 0.0225 |
| Top 3 | KNN | 0.9899 | 0.9943 | 0.999 | 1 | 0.9887 | 0.023 | -0.001 |
| Top 3 | LogReg | 0.9984 | 0.9933 | 0.9989 | 1 | 0.9878 | 0.0221 | 0.0075 |
| Top 3 | DecisionTree | 0.9985 | 0.9792 | 0.9964 | 1 | 0.9887 | 0.008 | 0.0076 |
| Top 3 | GaussianNB | 0.9909 | 0.9713 | 0.9951 | 0.9772 | 0.967 | 0 | 0 |

### Baseline (Naive Bayes) — Validation Snapshot
- Threshold: **0.9806**
- PR-AUC: **0.9775**, Accuracy: **0.9867**
- Precision / Recall / F1: **0.9028 / 0.9452 / 0.9235**
- Valid positive rate: **0.0849** • Pred pos rate: **0.0889**
- Confusion (valid): **TN=279,230  FP=2,660  FN=1,433  TP=24,712**

## Task 1B — Service Similarity
### Nearest Neighbors (baseline cosine, sample of 10)
| service | n1 | s1 | n2 | s2 | n3 | s3 | n4 | s4 | n5 | s5 |
|:---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
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

### Nearest Neighbors (PCA(3) cosine, sample of 10)
| service | n1 | s1 | n2 | s2 | n3 | s3 | n4 | s4 | n5 | s5 |
|:---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| ABTEST | DYNPRC | 0.999998917249505 | NOTIFY | 0.9999952321316882 | XCHATTR | 0.999971045934221 | RECV2 | 0.9993283148194669 | DEMAND | 0.9989205802256751 |
| AIRFLW | KAFKA | 0.9976439139043473 | AZURE | 0.9973345870085293 | AWS | 0.9912035166597828 | DBRCKS | 0.9834457867635032 | SNWFLK | 0.9746494920754835 |
| ANALAPI | ECOMLP | 0.9981805686152632 | RISKMG | 0.997183262025705 | MOBAPP | 0.9971430043707528 | GLOBCMP | 0.9967874023901064 | SUPCHN | 0.9958319909395957 |
| APIGWY | SNAPINT | 0.9999983536345758 | MKTDB | 0.992356942570567 | SLSDB | 0.9923448008086486 | MULTILNG | 0.9873527880185329 | DATARES | 0.9867762529126265 |
| ATLAS | MDLREG | 0.9740936935639666 | GEOANL | 0.9668142544896832 | FRDETCT | 0.947678468494115 | MCSCBT | 0.9308126398598165 | FEATSTR | 0.9287963659539529 |
| AUTOML | PAYPROC | 0.9999689621264357 | FINRPT | 0.9995899474130631 | BILLING | 0.9986211657004764 | GLOBAGG | 0.9985395450442296 | WHLSLP | 0.9978496112275563 |
| AWS | AIRFLW | 0.9912035166597828 | KAFKA | 0.9868388423555405 | DBRCKS | 0.9851093174394467 | AZURE | 0.9830383306331658 | SNWFLK | 0.9543345030669141 |
| AZURE | KAFKA | 0.9996268478421717 | AIRFLW | 0.9973345870085293 | SNWFLK | 0.988047155234139 | DBRCKS | 0.9873627689130235 | AWS | 0.9830383306331658 |
| BILLING | GLOBAGG | 0.9997452783398493 | SUPCHN | 0.9997417530359245 | GLOBCMP | 0.999423977933926 | RISKMG | 0.9992451481628609 | AUTOML | 0.9986211657004764 |
| CHURNP | FINPLAN | 0.9999995279190628 | INVOPT | 0.9931236472843021 | TRNPIPE | 0.9927190723593805 | FEATSTR | 0.9875157175652994 | EXCS | 0.9813653871817014 |

### Clustering Sweep (Silhouette over k)
| Representation | Method | k | Silhouette |
|:---|:---:|:---:|:---:|
| Role means (8-d) | KMeans | 3 | 0.851158675092405 |
| Role means (8-d) | KMeans | 4 | 0.8687091680037328 |
| Role means (8-d) | KMeans | 5 | 0.933113627229332 |
| Role means (8-d) | KMeans | 6 | 0.9661969420545483 |
| Role means (8-d) | KMeans | 7 | 0.9631850236343544 |
| Role means (8-d) | KMeans | 8 | 0.9834557457986388 |
| Role means (8-d) | KMeans | 9 | 0.9743887732550746 |
| Role means (8-d) | KMeans | 10 | 0.9673060323981396 |
| Role means (8-d) | Agglomerative(avg, cosine) | 3 | 0.851158675092405 |
| Role means (8-d) | Agglomerative(avg, cosine) | 4 | 0.8820796951992097 |
| Role means (8-d) | Agglomerative(avg, cosine) | 5 | 0.933113627229332 |
| Role means (8-d) | Agglomerative(avg, cosine) | 6 | 0.9661969420545483 |
| Role means (8-d) | Agglomerative(avg, cosine) | 7 | 0.9569899150823963 |
| Role means (8-d) | Agglomerative(avg, cosine) | 8 | 0.9834557457986388 |
| Role means (8-d) | Agglomerative(avg, cosine) | 9 | 0.9743887732550746 |
| Role means (8-d) | Agglomerative(avg, cosine) | 10 | 0.9570967842094384 |

- Best: **Role means (8-d)** • **KMeans** at **k=8** (Silhouette=0.9835)

### Task 3 – Feature Refinement (summary)
- Best so far: **KNN_k=11** — F1=0.9943, PR-AUC=0.9923, Acc=0.999, Prec=1, Rec=0.9887, Thr=0.2715
_See `task3_feature_refinement_results.csv` for full sweep._

## Key Takeaways
- KNN and Logistic Regression outperform GaussianNB on both feature sets; largest gains in F1 and PR-AUC.
- Top-3 features `[req_count, cost_sum, cost_mean]` are highly predictive; simple models already excel.
- For similarity, cosine baseline is strong; KMeans/Agglomerative produce compact clusters (best near k≈8).

## Next Steps
1) Lock in best contender configs for final write-up.
2) Add figures (PR curves, confusion heatmap, cluster diagram) as time permits.
3) Begin Bonus-task investigation plan.