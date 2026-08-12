# Current Methodology and Proposed Research Model

## 1. Version boundary

- **Production heuristic v1 - `IMPLEMENTED`:** the current EduPulse scoring and heatmap logic.
- **Research model v0 - `PROPOSED`:** Paper 1 prototype; it is not assumed to be superior before benchmarking.

Any production change during data collection requires event/model versioning and a recorded rollout boundary.

## 2. Production page/session score

For page threshold `T` from metadata or the 180-second fallback:

```text
dwell_raw = min(dwell_seconds / T, 1)
scroll = min(scroll_reversals / 6, 1)
selection = min(text_selection_count / 4, 1)
hover = min(hover_count / 12, 1)
```

Idle dwell at or above 120 seconds is multiplied by `0.1`; idle-only evidence is capped. A false-positive profile applies attenuation `a in [0,1]` to implicit components. Explicit event counts are converted to presence indicators in one payload.

The current score is:

```text
C_page = clip_[0,1](
    0.20 * dwell * a
  + 0.30 * scroll * a
  + 0.12 * hover * a
  + 0.07 * selection * a
  + 0.40 * contextual_ai
  + 0.60 * direct_chat
  + 0.50 * negative_feedback
  + 0.30 * annotation
  + 0.15 * text_signal_strength
)
```

Weights are configurable and must be logged with the research baseline version.

Positive/review-oriented typed notes without question/stuck cues are routed to engagement: heatmap confusion weight falls from `2.5` to `0.2`. This is a rule-based mitigation, not yet a validated multilingual classifier.

The current confidence field is an evidence-quality heuristic based on active channels and flags. It is not a calibrated probability.

## 3. Production coordinate intensity

For events in a cell or page/day:

```text
I = alpha * (U / N_safe) * ln(1 + sum_i(w_i * exp(-lambda * age_i)))
```

- `U`: unique pseudonymous actors.
- `N_safe = max(class_size, U, 1)`; class fallback is `400`.
- `lambda = 0.1` per day.
- `alpha`: mean active material-level attenuation profile, fallback `1.0`.
- `ln(1 + ...)`: repeated-event damping.

| Action | Weight |
|---|---:|
| AI question/chat engagement | 3.0 |
| Text note | 2.5, or 0.2 for positive engagement |
| Flashcard fail | 2.0 |
| Draw/scribble | 1.8 |
| Visual lasso/note crop | 1.5 |
| Highlight | 1.2 |
| Dwell spike/page view | 1.0 |
| Text selection | 0.7 |
| Fallback | 0.5 |

These values are design choices, not cognitive constants. Paper 1 treats them as baseline hyperparameters and performs sensitivity/ablation analysis.

## 4. Proposed research model v0

### Input window

A student-page window contains up to `K` ordered events and the following feature families:

- categorical: event type/source/device/page/material/course;
- continuous: active dwell, reversals, speed, hover, normalized bbox and age;
- binary: idle, anomalous, explicit action and text availability;
- semantic: sanitized text embedding plus sentiment/intent;
- content: token/visual density and formula/table indicators;
- provenance: schema, client, model and prompt versions.

### Architecture

1. Event embeddings and normalized MLP features.
2. A one-directional GRU student-page sequence encoder.
3. An MLP spatial encoder for bbox and region-density features.
4. A permutation-invariant DeepSets cohort aggregator.
5. Separate heads for self-report difficulty, teacher bottleneck, quiz error and delayed exam risk.
6. A constructive-engagement head.
7. Per-head temperature scaling on a dedicated calibration split.

A Transformer is a challenger after the GRU baseline, not the default, because effective independent sample size may be much smaller than event count.

### Masked multi-task loss

```text
L_supervised = sum_k lambda_k * (
  sum_i m_ik * BCE(y_ik, p_ik) / max(sum_i m_ik, 1)
)

L = L_supervised
  + beta * L_engagement_separation
  + gamma * L_weight_decay
```

Missing labels are masked, never treated as negatives. Hyperparameters, thresholds and calibration temperatures are selected without test data.

### Output contract

The model returns versioned probabilities for all tasks, calibration method/version, uncertainty metadata, top evidence modalities, unique-student count and a sample-size warning. Instructor-facing output is cohort/page/region aggregate only.

## 5. Comparison contract

Required models are prevalence/no-skill, dwell-only, raw counts, the production heuristic, logistic regression, gradient-boosted trees, a single-task GRU and the proposed multi-task GRU+DeepSets model.

Required ablations remove micro-interactions, text, spatial features, temporal structure, content context, human calibration, unique-user correction and multi-task learning.

If the proposed model does not exceed the strong tabular baseline with credible intervals, the paper must emphasize construct/protocol/dataset findings rather than claim model superiority.

## 6. Explainability and reproducibility

Primary explanations are modality ablations, tabular permutation/SHAP analysis, de-identified event/region cases and explicit error categories. Attention weights are not causal explanations.

Reproducibility requires a frozen feature schema/data hash, immutable splits, at least three seeds, versioned configs, independent build/train/calibrate/evaluate commands, per-fold predictions, and experiment logs free of secrets, PII and raw private notes.
