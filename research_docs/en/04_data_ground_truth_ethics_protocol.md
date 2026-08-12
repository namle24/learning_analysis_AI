# Data, Ground Truth, and Ethics Protocol

## 1. Status and principles

This protocol is `PROPOSED`. Operational logs are not automatically research data.

The study follows purpose limitation, data minimization, identity/research separation, immutable provenance, participant withdrawal and aggregate reporting. No field is collected solely because it may be useful later.

## 2. Units of analysis

| Unit | Logical key | Purpose |
|---|---|---|
| Participant | `research_participant_id` | Pseudonymous study linkage |
| Session | participant + material + start | One learning visit |
| Event | immutable `event_id` | Atomic interaction |
| Window | participant + page + time range | Primary individual model input |
| Region | material + page + normalized geometry | Localization/cohort convergence |
| Label | target + source + granularity | Ground-truth observation |
| Assessment | item + participant + attempt | Near/delayed outcome |
| Intervention | course/page/action/time | Future causal study |

## 3. Versioned event contract

Each event records schema version, immutable ID, rotating research pseudonym, consent version, pseudonymous course/material, page, canonical/raw event type, UTC time, session, normalized geometry, behavioral values, sanitized derived text features and client/content/model provenance.

Research feature tables exclude email, student number, full IP, exact security fingerprint, access tokens and raw private notes.

## 4. Event semantics

| Family | Examples | Boundary |
|---|---|---|
| Passive | page view, active dwell, scroll | Weak reading/idle evidence |
| Attention | selection, hover, revisit | Local attention, not confusion proof |
| Active | highlight, scribble, lasso | Cognitive anchor or engagement |
| Constructive | typed note/self-explanation | Requires semantic interpretation |
| Help-seeking | contextual AI/direct chat | Strong explicit evidence; may be curiosity |
| Feedback | difficulty tag/comment | Explicit perception with quality checks |
| Assessment | quiz/exam attempt | Outcome, not momentary state |

Aliases map to canonical types while preserving the raw source type.

## 5. Ground-truth contract

A label stores pseudonymous participant when applicable, course/material/page/region, source (`SELF_REPORT`, `TEACHER`, `QUIZ`, `EXAM`), target, value/scale, capture time, referenced window, instrument version, pseudonymous rater and optional rater confidence.

Label sources remain separate heads. They are not majority-voted into one truth value.

## 6. Representative self-report sampling

Threshold-only prompts create verification bias. Research experience sampling therefore:

- stratifies heuristic windows into low `[0,0.35)`, medium `[0.35,0.75)` and high `[0.75,1]`;
- samples all strata, oversampling medium/high while retaining sampling probability;
- limits prompts to two per 45-minute session and at least 10 minutes apart;
- avoids the first 60 seconds and active typing/chat moments;
- records `random_stratum`, `high_trigger` or `control` reason;
- asks difficulty, confidence and whether the learner is carefully reading versus stuck.

Exact rates are usability-piloted and frozen before main collection. Inverse-probability weighting is available because the sampling probability is stored.

## 7. Teacher annotation

Teachers label page/region as `NO_BOTTLENECK`, `POSSIBLE_BOTTLENECK`, `CONFIRMED_BOTTLENECK` or `INSUFFICIENT_EVIDENCE`, with a pedagogical category.

Round A is blind to model score. Round B exposes model output for actionability assessment after labels are frozen. Reconsidered labels are appended with reasons rather than overwriting Round A.

At least 20% of sampled units receive independent double annotation when feasible. Report Cohen's kappa for nominal labels and weighted kappa for ordinal labels. Preserve raw ratings alongside adjudication.

## 8. Quiz and exam linkage

Before outcome collection, each item is mapped to course/topic/objective, material version, page/region, cognitive level, expected difficulty and timing. Store first-attempt correctness, attempts, latency and confidence where approved. Exam analysis should use item-level results rather than only total course score.

Generated quiz content is not automatically a validated assessment. Instructor review and item-quality checks are required.

## 9. Consent and communication

Participant information states what is collected, purpose, non-participation consequences, access roles, storage/retention, withdrawal, external AI processing, aggregate reporting, no grade impact and research/supervisor/ethics contacts.

Research consent is not bundled with mandatory course access and must not use dark patterns.

## 10. Privacy architecture

```text
Identity store -> restricted linkage vault -> de-identified research feature store
```

The linkage vault has separate access/audit logs. Pseudonyms rotate by study/course unless longitudinal linkage is approved. Raw text is sanitized before feature extraction. Security IP/device signals are excluded from learning models by default.

## 11. Retention and withdrawal

Institutional review sets legal durations. The working policy keeps linkage only through verification plus an approved grace period, keeps raw events only as long as needed for QA, deletes/tombstones participant-derived rows before final freeze upon valid withdrawal, and explains that already published aggregate statistics cannot be individually retracted.

## 12. Data-quality gates

Before training, report event distribution, unique participants/sessions, missingness, duplicates, clock skew, geometry validity, idle anomalies, consent reconciliation, label prevalence by sampling stratum and participant contribution concentration.

Stop if schema drift is unexplained, provenance is missing, consent reconciliation fails or identity/research separation is violated.

## 13. Release policy

After approval, the default release may contain de-identified feature tables, synthetic fixtures, schema, split manifests, data card, bias statement, license and metric-reproduction code.

It excludes raw private text, identifiers, IP/fingerprints, private handwriting/crops and small-cell aggregates. If release is not approved, publish code, schemas, synthetic data and a controlled-access plan.

## 14. Access roles

- Identity custodian: linkage and withdrawal only.
- Data engineer: approved pseudonymous events without direct identifiers.
- Research analyst: frozen features and labels.
- Instructor rater: assigned content/evidence without identity.
- External reviewer: aggregate artifacts or controlled access.

Every export records purpose, owner, timestamp and checksum.
