# Research Vision and Current EduPulse Status

## 1. Purpose

This document positions EduPulse as a **research platform** for Learning Analytics. It does not treat the current product as scientific novelty by itself. The long-term objective is to study how unresolved knowledge bottlenecks can be inferred from interactions with digital learning materials while preserving student privacy and agency.

Working title for Paper 1:

> **Human-Calibrated Multimodal Cognitive Bottleneck Detection from Learning Micro-Interactions**

The primary unit of interpretation is evidence of a bottleneck at a page or region within a cohort and time window. It is not a diagnosis that a named student is confused.

## 2. Product-to-research gap

| Layer | Current platform | Engineering value | Research requirement still missing |
|---|---|---|---|
| Capture | Dwell, scroll, hover, selection, notes, annotations, Ask AI, feedback, geometry | Multi-source traces in an authentic workflow | Consent, schema provenance, missingness and data-quality evidence |
| Analytics | Page score, spatial heatmap, ABSA, clustering | Deployed explainable baseline | Construct validity, learned model, uncertainty and external labels |
| Calibration | Confirmation popup and attenuation profile | Product false-positive loop | Held-out calibration study and selection-bias analysis |
| Outcomes | Flashcard/quiz generation and adaptive mock UI | Foundation for an action loop | Research-ready assessment attempts and item-topic-page mapping |
| Intervention | Teaching actions and AI insights | Instructor decision support | A causal study of learning impact |
| Privacy | RBAC, redaction, pseudonymous aggregates | Strong governance foundation | Research approval, retention, withdrawal and disclosure-risk review |

The potential contribution is therefore not “a dashboard.” It is a sensor-free, spatial, cohort-aware, time-aware, human-calibrated method evaluated against multiple sources of evidence.

## 3. Verified implementation boundary

### Telemetry and micro-interactions - `IMPLEMENTED`

- Course, material, page and session context.
- Active dwell plus idle and anomalous-dwell indicators.
- Scroll reversal/speed, hover and text-selection counts.
- Normalized selection geometry in `[0,1]`.
- Text notes, highlights, scribbles, lasso crops, Ask AI and feedback.
- Evidence breakdown, behavioral flags, signal kind and heuristic confidence.

### Confusion analytics - `IMPLEMENTED`

- Page/session scoring from implicit and explicit evidence.
- Idle decay and false-positive attenuation.
- Positive-note routing to engagement rather than confusion.
- Coordinate intensity using action depth, temporal decay, unique actors and logarithmic damping.
- Daily trends that reuse calibrated intensity.

### Human validation loop - implementation `VALIDATED`, scientific effect not yet validated

- Threshold-triggered confirmation popup.
- True-positive and false-positive responses.
- Local score correction and stored attenuation profiles.
- Validation records by user, course, material, page and time.

### Engineering evidence

The repository has unit and integration tests for scoring, heatmaps, validation, telemetry, privacy, RAG and APIs. These tests establish contract correctness. They do not establish that the construct is measured validly in real learners.

## 4. Scientific gaps

### Construct gap

Long dwell may indicate careful reading, inactivity, lecture listening or content complexity. Notes and highlights may indicate constructive engagement. Paper 1 therefore distinguishes:

- **Productive struggle:** difficulty followed by productive processing and adequate outcomes.
- **Unresolved bottleneck:** persistent/repeated difficulty or help-seeking associated with poor outcomes.
- **Engagement anchor:** active interaction without evidence of unresolved difficulty.
- **Noise:** idle, accidental, spammed or context-poor activity.

### Label gap

Self-report is timely but response-biased. Teacher labels are pedagogically meaningful but often cohort/page-level. Quiz performance measures a near-term knowledge gap and depends on item quality. Exam outcomes are delayed and confounded. These sources must remain separate tasks rather than a single majority-voted truth column.

### Modeling gap

The production model uses hand-set weights and windowed aggregates. It does not learn event sequences, estimate calibrated uncertainty from real labels, or demonstrate cross-course generalization.

### Evaluation gap

Missing evidence includes grouped temporal splits, strong baselines, full ablations, calibration metrics, teacher reliability, assessment linkage and external-course validation.

### Governance gap

Possession of operational logs does not imply research consent. Approval, participant information, withdrawal, retention and access rules precede publication-oriented analysis.

## 5. Multi-stage research program

| Stage | Main question | Artifact | Permitted claim |
|---|---|---|---|
| Paper 1 | Do micro-interactions and human calibration improve bottleneck detection? | Method, approved features, benchmark, ablation | Detection, calibration and construct validity |
| Paper 2 | Do hotspot-informed actions improve learning? | Prospective or stepped-wedge intervention | Pedagogical/causal impact |
| Paper 3 | Does the model generalize across institutions and contexts? | Domain adaptation or multi-institution study | Robustness/generalization |

Paper 1 must not claim intervention effectiveness.

## 6. Six-week readiness criteria

1. A bilingual protocol, paper blueprint and claim registry exist.
2. Every planned field has purpose, owner, retention and provenance.
3. Synthetic replay covers event to feature to model to metric.
4. The current heuristic is reproducible as a frozen baseline.
5. The prototype has a fixed interface, loss, split and evaluation contract.
6. No claim becomes `VALIDATED` without recorded evidence.
7. A professor can make a go/no-go decision without guessing what remains unfinished.

## 7. Principal risks

| Risk | Consequence | Mitigation |
|---|---|---|
| Consent selection bias | Non-representative sample | Report consent process and permitted opt-in/opt-out aggregates |
| Sparse labels | Model learns frequent responders | Multi-task labels, stratified sampling and prevalence reporting |
| Leakage | Inflated performance | Student/course/material grouping and temporal holdout |
| Pseudoreplication | Raw event count overstates N | Cluster bootstrap and mixed-effects analysis |
| Productive-struggle false positives | Misleading intervention | Engagement head and outcome linkage |
| Single-course evidence | Weak generalization | Leave-one-course-out when 3-5 courses are available |
| Privacy encroachment | Loss of trust and approval | Data minimization, aggregate output and pre-collection ethics gate |

## 8. Progress reporting

Progress is reported per artifact using `Artifact | Status | Evidence | Blocker`. A global percentage is not used because it hides research-critical missing evidence.
