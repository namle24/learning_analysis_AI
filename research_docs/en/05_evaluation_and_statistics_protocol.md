# Evaluation and Statistical Protocol

## 1. Evaluation questions

Evaluation separately measures discrimination, probability calibration and educational validity. No single score substitutes for all three.

## 2. Splits and leakage controls

- Freeze immutable split manifests before training.
- Keep all events from one participant in one fold.
- Report participant-grouped and content/course-held-out settings.
- Use inner validation only for tuning.
- Keep calibration data separate from training and test.
- With at least three courses, use leave-one-course-out outer evaluation, participant-grouped chronological inner splits and a final prospective holdout after model freeze.
- A one-course pilot is internal validation only.

## 3. Required baselines

| ID | Model |
|---|---|
| B0 | Prevalence/no-skill |
| B1 | Active dwell plus idle |
| B2 | Raw event counts |
| B3 | Production heuristic |
| B4 | Logistic regression |
| B5 | Gradient-boosted trees |
| B6 | Single-task GRU |
| M1 | Multi-task GRU + spatial encoder + DeepSets |

All models use the same split and label-availability masks.

## 4. Ablations

Pre-register `-micro`, `-text`, `-spatial`, `-temporal`, `-content`, `-human-calibration`, `-unique-user` and `single-task`. Report all planned ablations, including negative results.

## 5. Metrics

### Classification

AUPRC is primary under imbalance. Report AUROC, macro-F1, sensitivity, specificity, confusion matrix and precision/FPR at a validation-selected recall target. The planning default is recall `0.80`, subject to teacher agreement before preregistration.

### Calibration

Report Brier score, ECE with declared bins, reliability diagrams, calibration slope/intercept when supported, and pre/post temperature-scaling results.

### Localization

Use region IoU, normalized center distance, Recall@K/pointing hit and page-level AUPRC when region labels are sparse.

### Temporal/operational utility

Report detection lead time, alert stability, alerts per instructor-week, false alerts per 100 student-hours, evidence sufficiency and blinded actionability ratings.

## 6. Statistical inference

- Report 95% confidence intervals.
- Use at least 1000 participant-cluster bootstrap resamples; preserve course hierarchy when available.
- Compare paired predictions on the same test units.
- Use mixed-effects logistic models with participant and item/course random intercepts where appropriate.
- Apply Holm correction within ablation families.
- Report effect sizes and uncertainty, not p-values alone.
- Use pilot data for prevalence/ICC/power estimation, not confirmatory testing.

## 7. Effective sample size

The 300-1000-student target does not guarantee power because repeated windows are clustered. After pilot collection, estimate prevalence, windows per participant, intra-class correlation and a minimum relevant AUPRC/Brier improvement, then run simulation-based power analysis. Report both raw windows and independent units.

## 8. Missing labels

Task masks treat missing labels as missing, not negative. Report availability by course, score stratum and activity level. Use inverse-probability weighting for sampled self-reports and compare complete-case with weighted sensitivity analyses. Never impute an evaluation label using the tested model.

## 9. Fairness and robustness

Only approved, educationally justified attributes are audited. Suppress small cells, include intervals and examine consent/missingness disparity before model disparity.

Robustness scenarios include duplicate spam, idle dwell, accidental selection, positive notes, mixed-language questions, changed materials, missing geometry/text, varied class size and upstream sentiment/embedding version changes.

## 10. Error taxonomy

Analyze productive-struggle false positives, silent-confusion false negatives, content-complexity false positives, curiosity-driven AI questions, rater disagreement and incorrect outcome mapping. When sample permits, inspect at least 20 stratified TP/FP/FN/TN cases across courses.

## 11. Experiment manifest

Every experiment records data/split/label/feature/model versions, seeds, calibration, primary metric and threshold policy. Per-fold predictions must be retained so all metrics and confidence intervals can be recomputed.

## 12. Acceptance gate

The prototype is research-ready when B0-B6 and M1 run on identical frozen splits, leakage checks pass, calibration excludes test labels, reports include intervals/ablations/failures and the claim registry is updated.

Model superiority requires the preregistered primary comparison to exceed its minimum relevant difference without a serious calibration or false-alert regression.
