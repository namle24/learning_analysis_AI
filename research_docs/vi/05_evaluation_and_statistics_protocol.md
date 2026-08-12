# Protocol evaluation và thống kê

## 1. Mục tiêu

Evaluation phải trả lời ba câu riêng:

1. **Discrimination:** model xếp positive cao hơn negative tới mức nào?
2. **Calibration:** xác suất dự đoán có khớp tần suất đúng không?
3. **Educational validity:** prediction có liên hệ với teacher bottleneck và learning outcomes không?

Không dùng một metric tổng hợp để che ba câu này.

## 2. Dataset partition và leakage control

### Development phase

- Tạo immutable split manifest trước training.
- Mọi event của cùng participant nằm trong cùng fold ở một experiment.
- Material/page version có thể tạo content leakage; report cả participant-grouped và material/course-held-out setting.
- Hyperparameter tuning chỉ dùng inner validation.
- Calibration set tách khỏi training và test.

### Primary generalization design

Khi có ít nhất ba course:

- Outer evaluation: leave-one-course-out.
- Inner split trong training courses: grouped theo participant và chronological cutoff.
- Final prospective holdout: collection period sau khi model/config đã freeze.

Nếu chỉ có một course ở pilot, kết quả được gọi là internal validation, không claim cross-course generalization.

## 3. Baselines

| ID | Baseline | Inputs |
|---|---|---|
| B0 | Prevalence/no-skill | Không dùng feature |
| B1 | Dwell-only | Active dwell + idle flag |
| B2 | Raw count | Event counts không weighting |
| B3 | Production heuristic | Current page score/heatmap formula |
| B4 | Logistic regression | Frozen tabular features |
| B5 | Gradient-boosted trees | Cùng tabular features |
| B6 | Single-task GRU | Ordered event sequence |
| M1 | Proposed multi-task GRU + DeepSets | Sequence + spatial + cohort + content + text features |

Mọi model dùng cùng split và label availability mask.

## 4. Ablation matrix

| Ablation | Câu hỏi |
|---|---|
| `-micro` | Highlight/note/draw/selection có incremental value không? |
| `-text` | Sanitized semantic features có giúp ngoài event type không? |
| `-spatial` | Geometry/cohort overlap có giúp localization không? |
| `-temporal` | Event order/time decay có giúp ngoài aggregate không? |
| `-content` | Slide complexity có giảm false positive dwell không? |
| `-human-calibration` | Self-report calibration có giảm false alerts không? |
| `-unique-user` | Chống spam theo distinct participant có cần thiết không? |
| `single-task` | Multi-source tasks có cải thiện robustness không? |

Không chỉ báo cáo ablation tốt; toàn bộ matrix preregister phải xuất hiện trong appendix/artifact.

## 5. Metrics

### Classification

- AUPRC là metric chính khi positive hiếm.
- AUROC, macro-F1, sensitivity, specificity là metric phụ.
- Precision/false-positive rate tại recall target. Default planning target là recall `0.80`; teacher review có thể đổi trước preregistration.
- Confusion matrix ở threshold đã khóa trên validation.

### Calibration

- Brier score.
- Expected Calibration Error với binning được khai báo.
- Reliability diagram.
- Calibration slope/intercept nếu sample cho phép.
- Pre/post temperature-scaling comparison.

### Localization

- Region IoU khi teacher có bbox/polygon.
- Center distance chuẩn hóa theo page diagonal.
- Pointing-game hit hoặc Recall@K hotspot.
- Page-level AUPRC nếu region labels quá thưa.

### Temporal usefulness

- Lead time giữa first reliable alert và teacher/quiz evidence.
- Time-to-detection survival summary.
- Stability theo consecutive windows; tránh alert nhấp nháy.

### Utility và workload

- Alerts per instructor/week.
- False alerts per 100 student-hours.
- Proportion alerts có đủ sample/evidence.
- Teacher actionability rating ở blinded second-round review.

## 6. Statistical inference

- Point estimate luôn kèm 95% confidence interval.
- Cluster bootstrap tối thiểu 1000 resamples ở participant; nếu nhiều course, resample có hierarchy course -> participant.
- So sánh paired predictions trên cùng test units.
- Mixed-effects logistic model cho outcome với random intercept participant và item/course khi phù hợp.
- Holm correction cho family ablation comparisons.
- Báo cáo effect size và uncertainty, không chỉ p-value.
- Pilot dùng để ước lượng prevalence/intra-class correlation; không dùng pilot test result làm confirmatory result.

## 7. Sample-size và effective N

Target 300-1000 sinh viên không tự động đảm bảo power vì event lặp lại trong cùng participant/course.

Sau pilot cần:

1. Ước lượng positive prevalence theo label source.
2. Ước lượng events/windows trên participant và intra-class correlation.
3. Chọn minimum-relevant improvement trên AUPRC/Brier.
4. Chạy simulation-based power theo clustered design.
5. Chốt số participant/course cần thiết trước collection chính.

Report cả raw windows và effective independent units.

## 8. Missing labels

- Multi-task loss dùng task mask; không coi missing là negative.
- Báo cáo label availability theo course, score stratum và participant activity.
- Dùng inverse-probability weighting cho self-report sampling nếu sampling probability đã lưu.
- Sensitivity analysis giữa complete-case và weighted analysis.
- Không impute teacher/quiz label bằng chính model đang đánh giá.

## 9. Fairness và subgroup audit

Chỉ dùng attributes được ethics approval cho phép. Audit có thể gồm course, device class, language preference hoặc prior-performance band nếu có educational rationale.

- Không báo subgroup metric khi cell quá nhỏ.
- Báo confidence interval và coverage, không rank cá nhân.
- Kiểm tra consent/missingness disparity trước model disparity.
- Nếu disparity lớn, phân tích data process trước khi thêm fairness regularizer.

## 10. Robustness tests

- Duplicate/spam events.
- Long idle dwell.
- Accidental text selection.
- Positive/review note chứa từ khóa tích cực.
- Mixed Vietnamese-English question.
- New material version.
- Missing geometry/text modality.
- Course with different class size.
- Provider/model version change cho sentiment embedding.

## 11. Error taxonomy

| Error | Ví dụ | Investigation |
|---|---|---|
| Productive-struggle FP | Nhiều note nhưng quiz đúng | Engagement/outcome head |
| Silent-confusion FN | Không tương tác nhưng quiz sai | Coverage limitation; không overclaim |
| Content-complexity FP | Slide dài làm dwell cao | Content-conditioned baseline |
| Curiosity FP | Ask AI mở rộng ngoài bài | Intent/semantic feature |
| Teacher disagreement | Raters đánh giá khác nhau | Reliability và adjudication |
| Outcome mismatch | Exam item map sai page | Item-map audit |

Mỗi model report có ít nhất 20 error cases được stratified theo TP/FP/FN/TN và course, nếu sample cho phép.

## 12. Experiment manifest

```yaml
experiment_id: research-v0-exp001
data_version: approved-feature-v1
split_manifest: split-v1.json
label_versions:
  self_report: sr-v1
  teacher: teacher-v1
  quiz: quiz-map-v1
features: feature-set-v1
model: multitask-gru-deepsets-v0
seeds: [17, 29, 43]
calibration: temperature-scaling
primary_metric: teacher_bottleneck_auprc
threshold_policy: validation_recall_0.80
```

## 13. Acceptance gates

Prototype được xem là research-ready khi:

- Pipeline chạy lại từ frozen input tới report.
- B0-B6 và M1 dùng cùng split.
- Không có participant/material leakage theo manifest.
- Calibration không dùng test labels.
- Metric có CI và per-fold predictions.
- Claim registry được cập nhật theo evidence.

Model chỉ được gọi là superior khi primary comparison đã preregister vượt minimum-relevant delta với CI phù hợp và không tạo regression nghiêm trọng ở calibration/false-alert workload.
