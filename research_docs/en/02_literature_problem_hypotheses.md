# Literature, Problem Formulation, and Hypotheses

## 1. Review status

The shared [literature matrix](../literature_matrix.csv) is a scoping seed, not a completed systematic review. The final Related Work section requires dated searches, database/query logs, inclusion/exclusion rules, independent screening and retained exclusion reasons.

## 2. Theoretical position

### Confusion is not uniformly harmful

Cognitive-affective research shows that confusion may support learning when resolved and become harmful when it persists or transitions into frustration/disengagement. EduPulse therefore targets **unresolved cognitive bottlenecks**, not a generic negative state.

### Observable action is not latent cognition

ICAP separates passive, active, constructive and interactive engagement. A note, highlight or AI question has different active effort, but none is automatically confusion. The model needs an engagement target, semantic context and downstream outcomes.

### Sensor-free affect detection is established prior work

Prior studies combine clickstream, language and fine-grained logs. Novelty cannot be “behavior plus text.” The candidate contribution is the combination of spatial anchors, ordered micro-interactions, cohort convergence, human false-positive calibration, multi-source outcomes and privacy-aware authentic deployment.

### Calibration is operationally important

Instructor-facing probabilities should correspond to observed frequencies. Paper 1 therefore reports Brier score, ECE and reliability diagrams in addition to discrimination. No threshold or calibration parameter is selected on the test set.

### Ethics is part of the method

Multimodal learning analytics can become surveillance. Consent, minimization, access boundaries, withdrawal and learner agency are first-class study-design elements.

## 3. Formal problem

Given students `S`, learning material `M`, page/region `R`, and time-ordered events `E`, estimate:

1. `p_individual`: evidence that a student-page window contains unresolved difficulty.
2. `p_cohort`: evidence that a page/region is a cohort bottleneck requiring review.

The system must separate engagement from difficulty, preserve temporal/spatial/content context, produce calibrated uncertainty, generalize across students/materials/courses, avoid biometric sensors, and expose only approved aggregate outputs.

## 4. Research questions

- **RQ1 Incremental validity:** Do micro-interactions improve detection over dwell/page-view telemetry?
- **RQ2 Human calibration:** Do false-positive feedback and multi-source supervision improve calibration and reduce false alerts without unacceptable recall loss?
- **RQ3 Spatial-cohort validity:** Does multi-student convergence at a region predict teacher-confirmed bottlenecks and assessment errors better than raw counts?
- **RQ4 Deferred:** Do bottleneck-informed interventions improve learning outcomes?

## 5. Pre-registration hypotheses

| ID | Hypothesis | Primary comparison | Primary evidence |
|---|---|---|---|
| H1 | Multimodal detection exceeds dwell-only | Proposed vs dwell-only | AUPRC difference and CI |
| H2 | Micro-interactions add incremental value | Full vs `-micro` | AUPRC and Brier |
| H3 | Human calibration reduces false alerts | Calibrated vs uncalibrated | FPR at fixed recall and ECE |
| H4 | Unique-user spatial aggregation exceeds raw counts | Spatial cohort vs count | Region AUPRC/IoU |
| H5 | Signals predict near outcomes better than delayed outcomes | Quiz vs exam tasks | AUPRC by temporal distance |
| H6 | Performance remains useful on unseen courses | Leave-one-course-out | Relative AUPRC drop |

Minimum relevant differences and tolerance margins are set from pilot prevalence/power simulation, then frozen before final testing.

## 6. Permitted novelty boundary

With complete evidence, Paper 1 may claim:

1. A cohort cognitive-bottleneck formulation for digital-material micro-interactions.
2. A multi-task temporal-spatial model that preserves label provenance.
3. A human calibration loop evaluated with calibration and workload metrics.
4. A privacy-aware prospective protocol/dataset artifact.

It must not claim mind reading, treat dwell as proof, assert top-tier novelty before the literature audit, claim learning improvement without an intervention, or generalize beyond the sampled context.

## 7. Literature search protocol

Sources: ACM DL, Scopus/Web of Science where available, ERIC, IEEE Xplore, SpringerLink, ScienceDirect and official LAK/EDM/AIED proceedings.

Core query families:

```text
(student confusion OR cognitive bottleneck OR productive struggle)
AND (learning analytics OR educational data mining)

(sensor-free affect detection OR interaction trace)
AND (student OR learner)

(multimodal learning analytics)
AND (calibration OR uncertainty OR ground truth)

(micro-interaction OR annotation OR text selection OR dwell time)
AND (learning OR reading)
```

Include peer-reviewed digital/classroom learning studies with explicit constructs, labels/outcomes or evaluation. Exclude unevaluated dashboard descriptions, marketing material, biometric-only work without transferable methods, and studies without target/label provenance.

Two reviewers independently screen the main set. Full-text exclusions retain reasons. The review is not called systematic until this protocol is completed.

## 8. Conceptual model

```text
Learning context
  -> observable micro-interactions
  -> latent processing state
  -> self-report / teacher interpretation / assessment outcome

Observable interaction != latent state != learning outcome
```
