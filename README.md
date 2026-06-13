# CompBioMed_Sem_B
## Introduction
Idiopathic ventricular arrhythmias originating in the cardiac outflow tracts (OTVAs) account for approximately 10% of all ventricular arrhythmias in patients without structural heart disease. They occur on either the left side of the heart (the left ventricular outflow tract, LVOT), including the aortic cusps (LCC, RCC and the LCC-RCC commissure) and the LVOT proper (Subvalvular and Summit subregions), or on the right side (the right ventricular outflow tract, RVOT), including the RVOT Septum and the RVOT Free Wall (RFW). Pre-procedural identification of the site of origin (SOO) is clinically valuable because it directly affects the catheter ablation approach: a left-sided origin requires retrograde aortic or transseptal access, whereas a right-sided origin can be approached more straightforwardly through the femoral vein.
The standard non-invasive tool for SOO inference is the 12-lead surface ECG, particularly the R/S transition across the precordial leads V1–V6. The most widely used clinical scoring system is the Hybrid Score proposed by Penela et al. [2], which combines clinical variables (sex, hypertension, age) with the precordial transition lead to produce a binary LVOT vs RVOT prediction. Reported accuracies for rule-based methods are in the range of 65–75%.
Recent work has applied machine learning to this problem. Notably, Bocanegra-Pérez et al. reported an F1-score of approximately 0.84 for binary classification using a convolutional architecture on a 43-patient cohort augmented by external datasets. Saglietto et al. demonstrated the broader applicability of lightweight CNNs for ECG analysis. These results motivate the use of deep learning, but multiclass extensions, distinguishing finer anatomical sublocations,  remain underexplored and structurally limited by the small size of clinical OTVA cohorts, a limitation explicitly identified by Doste et al. [5].
Our best models achieve F1 = 0.842 (Task 1), 0.726 (Task 2), and 0.258 (Task 3) on the held-out test set, with cross-validation gaps that confirm honest generalization. 

## Results Tables

Results for task 1:

| Model | Accuracy | F1-macro |
|---|---|---|
| Hybrid Score (Penela 2023, clinical) | 0.654 | 0.649 |
| Random Forest (Teknon, clinical+ECG) | 0.808 | 0.807 |
| CNN (Combined datasets, ECG only) | 0.846 | 0.842 |
| Ensemble RF + CNN (50/50) | 0.808 | 0.805 |

Results for task 2:

| Strategy | Acc | F1-macro |
|---|---|---|
| Trivial baseline (predict majority) | 0.423 | 0.198 |
| 1 - CNN from scratch | 0.577 | 0.53 |
| 2 - CNN Transfer Learning | 0.538 | 0.477 |
| 3 - Hard Hierarchical Cascade | 0.692 | 0.689 |
| 4 - Soft Cascade ⭐ | 0.731 | 0.726 |
| 5 - PCA + HistGradientBoosting Cascade | 0.577 | 0.51 |
| 6 - Expanded Pool (DS-2496 synthetic) | 0.5 | 0.435 |
| 7 - Classical: Logistic Regression | 0.385 | 0.338 |
| 7 - Classical: SVM (RBF kernel) | 0.5 | 0.428 |
| 7 - Classical: Random Forest | 0.577 | 0.515 |

Results for task 3:


| Strategy | Acc | Macro F1 |
|---|---|---|
| Trivial baseline (predict majority class) | 0.192 | 0.046 |
| 1 - Multimodal ResNet Ensemble | 0.346 | 0.249 |
| 2 - Linear SVM + SelectKBest | 0.308 | 0.229 |
| 3 - Late-Fusion (ResNet + SVM, 50/50) | 0.346 | 0.258 |
