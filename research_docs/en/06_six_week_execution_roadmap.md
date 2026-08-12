# Six-Week Execution Roadmap

## 1. End state

The six-week outcome is a research-readiness package and reproducible prototype, not a completed paper based on unapproved data.

Three workstreams operate with one accountable owner and one cross-reviewer per artifact:

- **Research/Method Lead:** constructs, literature, hypotheses, model and paper story.
- **Data/Platform Lead:** schema, provenance, synthetic replay, features and reproducibility.
- **Evaluation/Governance Lead:** ethics, labels, annotation, metrics, statistics and claims.

## 2. Week 1 - Framing and audit

Freeze the product SHA/schema inventory, complete code-to-claim mapping, run the first literature screen, define productive struggle/bottleneck/engagement/noise, and lock draft RQs/hypotheses.

Deliver research vision, literature matrix/search log, claim registry and architecture diagram. Exit only when every claim has status and novelty is distinguishable from prior behavior-plus-text work.

## 3. Week 2 - Governance and contracts

Draft participant information, consent/withdrawal, identity separation, event/label schemas, self-report instrument, teacher handbook and assessment mapping.

Exit only when every field has purpose/owner, consent state is explicit, and label sources/granularities remain separate.

## 4. Week 3 - Synthetic replay and baselines

Create a multi-course synthetic sequence/geometry/label dataset, validators, feature schema, split manifests, B0-B5 implementations, frozen production heuristic and experiment manifests.

Exit when a clean checkout reproduces event -> feature -> baseline -> report, leakage tests pass and golden fixtures match production scoring.

## 5. Week 4 - Proposed prototype

Implement event encoder, GRU, spatial encoder, DeepSets aggregator, masked multi-task/engagement heads, calibration and versioned outputs. Run at least three seeds on synthetic or approved fixtures.

Exit when missing labels/modalities work, test data does not influence tuning and the output contract is stable.

## 6. Week 5 - Evaluation dry run

Run baseline/ablation matrices, clustered bootstrap, calibration reports, annotation dry runs, stratified sampling simulation and error/subgroup templates.

Exit when metrics reproduce from per-unit predictions, negative cases are documented and missing evidence for the real study is explicit.

## 7. Week 6 - Readiness review

Synchronize Vietnamese/English documents, finalize Paper 1 figures/tables, run adversarial claim review, prepare a 15-minute professor briefing and conduct a pilot go/no-go review.

`GO` requires professor alignment, an identified ethics route/data owner, feasible labels, demonstrated technical feasibility and no critical leakage/privacy blocker. Otherwise select `ITERATE`; do not collect real research data to satisfy an artificial deadline.

## 8. Working rhythm and DoD

Monday locks the weekly hypothesis/artifacts/owners; mid-week cross-review updates blockers; Friday demonstrates artifacts rather than descriptive slides; week-end updates the claim registry and version tag.

An artifact is complete only when it has reviewable evidence: search logs for literature, provenance/validator for schemas, commands/config/splits/predictions for models, intervals/calibration/failures for evaluation, and withdrawal/retention/access/provider disclosure for ethics.

## 9. Contingencies

- No ethics route by Week 2: synthetic-only work.
- No outcome mapping: teacher/self-report become primary; assessment remains secondary future validation.
- One course only: internal pilot, no generalization claim.
- Sparse labels: adjust stratified sampling without redefining positives.
- Proposed model loses to XGBoost: emphasize construct/protocol/dataset or simplify the model.
- No release approval: publish code, schema, synthetic data and controlled-access procedure.
