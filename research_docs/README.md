# EduPulse Learning Analytics Research Program

This directory turns EduPulse from a product implementation into a research-ready program. It does not claim that the current product, heuristic confusion score, or existing test suite is already a scientific contribution.

## Research position

**Working Paper 1 title:** *Human-Calibrated Multimodal Cognitive Bottleneck Detection from Learning Micro-Interactions*

**Primary community:** Learning Analytics / Educational Data Mining (LAK, EDM, JEDM).

**Six-week objective:** research-readiness protocol plus a reproducible prototype on synthetic or explicitly approved data. Six weeks is not treated as a paper-submission deadline.

**Longer-term study target:** 3-5 courses/classes and approximately 300-1000 students, subject to institutional approval, informed consent, and a power analysis based on pilot prevalence.

## Claim status vocabulary

Every research document uses the following labels.

| Label | Meaning |
|---|---|
| `IMPLEMENTED` | The behavior exists in the current repository and is traceable to code or schema. |
| `VALIDATED` | The implementation has recorded test/evaluation evidence. This does not automatically imply external or scientific validity. |
| `PROPOSED` | The method, interface, study, or model is specified but not yet implemented or evaluated. |
| `FUTURE` | Deferred beyond Paper 1 or the six-week readiness gate. |

The canonical machine-readable registry is [claim_evidence_registry.csv](./claim_evidence_registry.csv).

## Document map

| Topic | Vietnamese | English |
|---|---|---|
| Research vision and current status | [VI-01](./vi/01_research_vision_and_status.md) | [EN-01](./en/01_research_vision_and_status.md) |
| Literature, problem, and hypotheses | [VI-02](./vi/02_literature_problem_hypotheses.md) | [EN-02](./en/02_literature_problem_hypotheses.md) |
| Current and proposed methodology | [VI-03](./vi/03_methodology_current_and_proposed.md) | [EN-03](./en/03_methodology_current_and_proposed.md) |
| Data, ground truth, and ethics | [VI-04](./vi/04_data_ground_truth_ethics_protocol.md) | [EN-04](./en/04_data_ground_truth_ethics_protocol.md) |
| Evaluation and statistics | [VI-05](./vi/05_evaluation_and_statistics_protocol.md) | [EN-05](./en/05_evaluation_and_statistics_protocol.md) |
| Six-week execution roadmap | [VI-06](./vi/06_six_week_execution_roadmap.md) | [EN-06](./en/06_six_week_execution_roadmap.md) |
| Paper 1 blueprint | [VI-07](./vi/07_paper_1_blueprint.md) | [EN-07](./en/07_paper_1_blueprint.md) |

Shared artifacts:

- [Research system diagram](./research_system.mmd)
- [Initial literature matrix](./literature_matrix.csv)
- [Claim-evidence registry](./claim_evidence_registry.csv)

## Non-negotiable boundaries

1. Production telemetry collected without research consent is operational data, not automatically research data.
2. Dwell time is a weak contextual signal, not proof of confusion.
3. Self-report, teacher labels, quiz outcomes, and exam outcomes remain separate observations with different timing and granularity.
4. Paper 1 predicts cognitive bottleneck evidence; it does not diagnose a student's mental state.
5. Student-facing and instructor-facing outputs remain aggregate or pseudonymous unless an approved protocol explicitly allows otherwise.
6. Only de-identified feature-level data may be considered for release, and only after institutional approval and disclosure-risk review.

## Existing implementation evidence

The research dossier references, but does not duplicate, the following engineering documents:

- [Current confusion score](../architecture/calibrated_multimodal_confusion_score_vi.md)
- [Current architecture](../architecture/current_system_architecture.md)
- [Technical project status](../reports/technical_project_status_2026_07_02_vi.md)
- [Evaluation evidence](../evaluations/evaluation_evidence_full_2026_07_06_vi.md)
- [Telemetry specification](../specs/telemetry_ingestion.md)

These sources describe product behavior. Scientific claims require the additional protocol, data, baselines, and statistical evidence specified in this directory.
