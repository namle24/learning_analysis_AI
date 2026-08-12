# Roadmap triển khai sáu tuần

## 1. Mục tiêu cuối kỳ

Sau sáu tuần, team phải có **research-readiness package + reproducible prototype**, không phải một paper có kết quả thật nếu approval/consent chưa hoàn tất.

Ba workstream:

- **Research/Method Lead:** construct, literature, hypotheses, model specification và paper story.
- **Data/Platform Lead:** event schema, provenance, synthetic replay, feature pipeline và reproducibility.
- **Evaluation/Governance Lead:** ethics, ground truth, annotation, metrics, statistics và claim audit.

Mỗi artifact có một accountable owner; review chéo bởi ít nhất một workstream khác.

## 2. Week 1 - Research framing và audit

### Tasks

- Freeze product snapshot bằng git SHA và schema inventory.
- Hoàn thành code-to-claim audit cho telemetry, formula, calibration và outcomes.
- Chạy literature search protocol vòng đầu; deduplicate và screen.
- Khóa construct: productive struggle, unresolved bottleneck, engagement và noise.
- Draft RQ/Hypotheses và fatal-flaw review.

### Artifacts

- Research vision v1.
- Literature matrix v1 và search log.
- Claim-evidence registry v1.
- Current/proposed architecture diagram.

### Exit gate

- Mỗi claim có status.
- Không còn câu “dwell = confusion”.
- Novelty statement phân biệt được với clickstream+text prior work.

## 3. Week 2 - Governance và data contract

### Tasks

- Draft participant information, consent và withdrawal workflow.
- Xác định identity/research separation và data access roles.
- Freeze research event/label schema v1.
- Viết teacher annotation handbook và self-report instrument.
- Thiết kế quiz/exam item mapping.

### Artifacts

- Ethics/consent packet draft.
- Data dictionary và retention matrix.
- Ground-truth protocol.
- Annotation form/mock và adjudication log format.

### Exit gate

- Mọi field có purpose và owner.
- Không dùng production log nếu consent state không rõ.
- Label source/granularity không bị gộp.

## 4. Week 3 - Synthetic replay và baselines

### Tasks

- Tạo synthetic dataset có event sequence, geometry, missing labels và multiple courses.
- Tạo validator cho duplicate, missingness, timestamp và geometry.
- Freeze feature schema v1 và split manifest format.
- Reproduce B0-B5; bọc production heuristic thành frozen baseline.
- Tạo experiment manifest và deterministic seeds.

### Artifacts

- Synthetic dataset generator/spec.
- Data-quality report mẫu.
- Baseline report với per-fold predictions.
- Reproducibility commands.

### Exit gate

- Clean checkout có thể chạy synthetic event -> feature -> baseline -> report.
- Leakage tests pass.
- Heuristic baseline khớp code production trên golden fixtures.

## 5. Week 4 - Proposed model prototype

### Tasks

- Implement event encoder + GRU + spatial encoder + DeepSets aggregator.
- Implement masked multi-task heads và engagement head.
- Implement calibration split và temperature scaling.
- Export probabilities, uncertainty metadata và evidence summary.
- Chạy ít nhất ba seeds trên synthetic/approved fixtures.

### Artifacts

- Model card draft.
- Training/evaluation config.
- Prototype report, không dùng language “scientific improvement” trên synthetic data.

### Exit gate

- Model xử lý missing modalities/labels.
- Test labels không chảy vào tuning/calibration.
- Output contract ổn định và versioned.

## 6. Week 5 - Evaluation dry-run

### Tasks

- Chạy full baseline/ablation matrix trên synthetic/approved pilot.
- Chạy clustered bootstrap và calibration report.
- Dry-run teacher annotation trên synthetic/de-identified pages.
- Kiểm tra consent sampling/verification bias bằng simulated strata.
- Viết error taxonomy và subgroup/missingness report template.

### Artifacts

- Evaluation report skeleton có bảng/figure thật từ dry-run.
- Annotation reliability notebook/script.
- Risk register và unresolved decision log.

### Exit gate

- Mọi metric tái tạo từ per-unit predictions.
- Có failure case, không chỉ successful demo.
- Team biết chính xác data nào còn thiếu cho real study.

## 7. Week 6 - Research readiness review

### Tasks

- Đồng bộ bộ tài liệu Việt/Anh.
- Hoàn thiện Paper 1 skeleton, figures, expected tables và reviewer questions.
- Chạy adversarial claim-evidence review.
- Chuẩn bị 15-minute professor briefing và appendix kỹ thuật.
- Tổ chức go/no-go review cho pilot thật.

### Deliverables

- Research dossier versioned.
- Protocol/consent package sẵn sàng gửi institutional reviewer.
- Reproducible prototype bundle.
- Paper blueprint và publication-readiness rubric.
- Next-phase backlog có cost, owner-role và dependency.

### Go decision

Chỉ `GO` nếu:

- Professor/mentor đồng ý construct và contribution direction.
- Ethics route và data owner được xác định.
- Data/label pipeline khả thi.
- Prototype chứng minh technical feasibility.
- Không còn critical leakage/privacy blocker.

Nếu chưa đạt, chọn `ITERATE`; không thu data thật để chạy theo deadline.

## 8. Nhịp làm việc

| Thời điểm | Hoạt động |
|---|---|
| Monday | Khóa weekly hypothesis, artifacts và owner |
| Mid-week | Cross-review 30-45 phút, cập nhật blocker |
| Friday | Demo artifact, không demo slide mô tả |
| End week | Claim registry, decision log và version tag |

Mỗi thành viên 8-12 giờ/tuần; ưu tiên artifact có thể review hơn họp dài.

## 9. Definition of done theo artifact

| Artifact | Done khi |
|---|---|
| Literature matrix | Có query/date/source/screen reason và citation link |
| Data schema | Validator pass và mọi field có provenance |
| Baseline | Chạy từ command, lưu config/split/predictions |
| Model prototype | Ba seeds, no leakage, output versioned |
| Evaluation | CI, calibration, ablation và failure cases |
| Ethics packet | Consent, withdrawal, retention, access và provider disclosure |
| Paper blueprint | Claim map tới table/figure/evidence |

## 10. Rủi ro và contingency

| Trigger | Điều chỉnh |
|---|---|
| Ethics route chưa rõ hết Week 2 | Chỉ synthetic data; tập trung protocol/prototype |
| Outcome mapping chưa có | Paper 1 primary target chuyển teacher/self-report, quiz là secondary future validation |
| Chỉ một course tham gia | Gọi internal pilot; không claim generalization |
| Label prevalence quá thấp | Tăng stratified sampling, không oversample bằng cách đổi label definition |
| Proposed model không hơn XGBoost | Định vị contribution vào construct/protocol/dataset hoặc đơn giản hóa model |
| Privacy review không cho release | Release code, schema, synthetic data và controlled-access plan |
