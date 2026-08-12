# Paper 1 Blueprint

## 1. Positioning

**Type:** Method plus empirical validation for Learning Analytics/EDM.

**Working title:** *Human-Calibrated Multimodal Cognitive Bottleneck Detection from Learning Micro-Interactions*

**One-sentence story:** EduPulse tests whether contextual sensor-free micro-interactions, aggregated across time, space and cohort and calibrated with multiple human evidence sources, detect instructional bottlenecks more reliably than conventional dwell/clickstream signals.

## 2. Logic chain

| Stage | Content |
|---|---|
| Background | Instructors detect digital-material bottlenecks too late. |
| Limitation 1 | Dwell/click proxies conflate inactivity, depth and difficulty. |
| Limitation 2 | Self-report, teacher and assessment labels differ in bias/granularity. |
| Limitation 3 | Detectors often lack calibration, spatial evidence and privacy-aware deployment. |
| Key idea | Model ordered micro-interactions with spatial-cohort aggregation and multi-source calibration. |
| Challenge 1 | Separate constructive engagement from unresolved difficulty. |
| Challenge 2 | Learn from sparse, noisy, heterogeneous labels. |
| Challenge 3 | Evaluate calibration/generalization without leakage or surveillance overclaim. |
| Module A | Event/sequence/content encoder and engagement head. |
| Module B | Spatial DeepSets aggregation and masked multi-task heads. |
| Module C | Held-out calibration, grouped evaluation and privacy-aware reporting. |

## 3. Conditional contributions

1. A cognitive-bottleneck formulation that separates engagement from difficulty.
2. A multi-task temporal-spatial cohort model with human calibration and uncertainty.
3. Multi-course empirical validation using self-report, teacher and assessment outcomes.
4. A de-identified feature dataset/protocol/code artifact if approved.

If only one course is available, Contribution 3 becomes internal prospective validation.

## 4. Paper structure

1. **Introduction:** late visibility, weak proxies, micro-interaction ambiguity, calibration/ground truth, bounded contributions.
2. **Related Work:** productive struggle, sensor-free traces, multimodal/spatial LA, calibration and privacy.
3. **Problem and Data:** constructs, units, context, governance, modalities, labels and missingness.
4. **Method:** production baseline, encoders, cohort aggregation, multi-task loss and calibration.
5. **Protocol:** splits, baselines, ablations, metrics, statistics and reproducibility.
6. **Results:** main comparison, calibration, ablation, generalization, localization, errors and fairness.
7. **Stakeholder Analysis:** annotation reliability, blinded actionability and alert workload.
8. **Discussion:** productive struggle, unobservable states, consent bias, limits and future intervention.

## 5. Planned figures and tables

Figures: a matched-dwell/different-outcome motivated example; the research pipeline; reliability curves; spatial predictions against teacher regions; and cross-course performance.

Tables: dataset/label statistics; baseline comparison with 95% CIs; ablations; calibration/workload tradeoffs; and error/subgroup coverage.

Dashboard screenshots are supporting system evidence, not the main methodology figure.

## 6. Abstract shell

```text
Detecting where learners encounter unresolved knowledge bottlenecks could
support timely teaching decisions, but common behavioral proxies such as
dwell time conflate difficulty with careful reading and inactivity. We study
[N] consenting students across [C] courses using privacy-preserving digital
material micro-interactions, including [...]. We introduce [...], a calibrated
multi-task model that [...]. Against [... baselines], the method [... verified
results only]. Ablations show [...], while cross-course and error analyses
identify [...]. These findings support [... bounded implication], without
treating behavioral traces as direct diagnoses of individual cognitive state.
```

No placeholder is replaced with an estimate or fabricated result.

## 7. Claim-evidence fallback

- Better detection requires the preregistered metric and CI; otherwise report comparable performance and evidence richness.
- Better calibration requires Brier/ECE/reliability evidence; otherwise state that calibration remains unresolved.
- Spatial value requires ablation and localization; otherwise call it qualitative anchoring.
- Generalization requires course holdout; otherwise state internal validation.
- Learning relevance requires assessment linkage; otherwise report contemporaneous-label association.
- Actionability requires blinded teacher review; otherwise describe design intent only.

## 8. Principal rejection risks

Heuristic-as-science, weak construct validity, leakage, one-course overclaim, inflated N, surveillance concerns, absent educational impact and unnecessary model complexity are addressed through strong baselines, multiple labels, immutable splits, cluster-aware statistics, aggregate outputs and bounded claims.

## 9. Venue and artifact strategy

The primary community is LAK/EDM/JEDM; a specific venue is selected after pilot and professor review. Six weeks is not forced into a submission deadline. Evidence quality determines whether the output is a full paper, short/workshop study, artifact/protocol contribution or continued internal work.

## 10. Reproducibility and adversarial review

The appendix includes data card/governance, schema, splits/leakage tests, hyperparameters/seeds/compute, permitted per-fold predictions, calibration, error taxonomy, annotation guide and model card.

This audit is mandatory before moving from the research specification to a paper draft.

| Review axis | Current status | Gate condition |
|---|---|---|
| Contribution/novelty | `PROPOSED`; novelty boundary is explicit | Mentor-reviewed literature matrix; every contribution maps to a result and closest baseline |
| Construct/method soundness | Production formula is traceable; research model is not implemented | Reproducible event contract, label provenance, missing-label loss, calibration and leakage tests |
| Experimental strength | Protocol exists; no approved empirical result | B0-B6/M1, ablations, at least three seeds, and course holdout or an internal-validation scope |
| Evaluation/statistics | Metrics, intervals and splits are specified | Primary AUPRC, Brier/ECE, cluster bootstrap, effective N, reliability/error/subgroup artifacts |
| Clarity/reproducibility | Bilingual dossier and claim registry exist | Introduction does not exceed Results; methods, manifests, configs, seeds and failures permit independent audit |
| Ethics/usefulness | Protocol-first; no institutional approval yet | Approved consent, withdrawal, identity separation, teacher actionability and alert-workload evidence |

**Decision rules:**

- Claim better detection only when the preregistered primary metric and confidence interval pass the gate.
- Claim better calibration only when Brier score, ECE and reliability evidence agree.
- Do not claim cross-course generalization without a course-level holdout.
- Do not claim improved learning without a suitable intervention or assessment linkage.
- Preserve negative results and narrow the contribution; never switch the primary metric after observing the test set.

Before professor review, an internal reviewer must confirm that every contribution maps to a figure/table/result, each major claim has registry status, Related Work includes the closest methods, Method is reproducible, experiments preserve failures/negative results, and ethics is documented at method level rather than as a generic disclaimer.
