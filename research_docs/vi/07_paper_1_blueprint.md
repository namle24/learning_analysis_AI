# Blueprint Paper 1

## 1. Paper positioning

**Type:** Method + empirical validation paper trong Learning Analytics/EDM.

**Working title:**

> Human-Calibrated Multimodal Cognitive Bottleneck Detection from Learning Micro-Interactions

**One-sentence story:**

> EduPulse nghiên cứu liệu các micro-interaction có ngữ cảnh, không dùng biometric sensor, khi được tổng hợp theo thời gian-vị trí-cohort và hiệu chuẩn bằng nhiều nguồn human evidence, có phát hiện bottleneck đáng tin cậy hơn dwell/clickstream truyền thống hay không.

## 2. Thinking template

| Stage | Nội dung |
|---|---|
| Background | Lớp học số tạo trace phong phú nhưng giảng viên thường nhận biết bottleneck quá muộn. |
| Limitation 1 | Macro click/dwell dễ nhầm idle, reading depth và difficulty. |
| Limitation 2 | Một nguồn label không đủ vì self-report, teacher và assessment khác granularity/bias. |
| Limitation 3 | Nhiều detector tối ưu discrimination nhưng thiếu calibration, spatial evidence và privacy-aware deployment. |
| Key idea | Mô hình hóa bottleneck bằng sequence micro-interaction đa phương thức, cohort-spatial aggregation và multi-source human calibration. |
| Challenge 1 | Tách productive engagement khỏi unresolved difficulty. |
| Challenge 2 | Học từ label sparse, noisy và khác granularity. |
| Challenge 3 | Đánh giá generalization/calibration mà không leakage hoặc surveillance overclaim. |
| Module A | Event/sequence/content encoder + engagement head. |
| Module B | Spatial DeepSets cohort aggregation + masked multi-task heads. |
| Module C | Held-out calibration, grouped evaluation và privacy-aware reporting. |

## 3. Contribution statements có điều kiện

Chỉ giữ contribution nếu corresponding evidence đạt gate:

1. **Problem/construct contribution:** formulation của cognitive bottleneck từ digital material micro-interactions, phân biệt engagement và difficulty.
2. **Method contribution:** multi-task temporal-spatial cohort model với human calibration và uncertainty.
3. **Empirical contribution:** evaluation trên 3-5 courses với self-report, teacher và assessment outcomes.
4. **Artifact contribution:** de-identified feature dataset/protocol/code nếu approval cho phép.

Nếu chỉ có một course, Contribution 3 phải đổi thành internal prospective validation.

## 4. Section skeleton

### 1. Introduction

1. Giảng viên thiếu visibility kịp thời trong digital reading.
2. Dwell/clickstream là weak proxies và dễ gây surveillance/false alerts.
3. Micro-interactions cung cấp cognitive anchors nhưng cũng có engagement ambiguity.
4. Ground truth đa nguồn và calibration là thách thức trung tâm.
5. Tóm tắt phương pháp và contributions có evidence.

### 2. Related Work

- Confusion/productive struggle và affect dynamics.
- Sensor-free affect detection và learning behavior traces.
- Multimodal/spatial learning analytics.
- Human-centered calibration, teacher decision support và privacy.

### 3. Problem and Data

- Construct definitions và prediction units.
- EduPulse study context.
- Consent/governance.
- Event modalities và label provenance.
- Dataset statistics/missingness.

### 4. Method

- Production heuristic baseline.
- Event and content encoding.
- Temporal-spatial cohort aggregation.
- Multi-task objectives.
- Calibration and uncertainty.

### 5. Experimental Protocol

- Splits/leakage controls.
- Baselines/ablations.
- Metrics/statistics.
- Reproducibility.

### 6. Results

- Main discrimination/calibration table.
- Ablation and generalization.
- Localization and lead time.
- Error/fairness analysis.

### 7. Teacher/Stakeholder Analysis

- Annotation reliability.
- Blinded actionability review.
- Workload/false-alert tradeoff.

### 8. Discussion

- Productive struggle interpretation.
- What model cannot observe.
- Privacy, consent bias và deployment boundary.
- Implications for future intervention study.

## 5. Planned figures

| Figure | Nội dung | Evidence source |
|---|---|---|
| Fig. 1 | Motivated example: same long dwell, different micro-interaction/outcome | Approved de-identified cases hoặc synthetic before approval |
| Fig. 2 | Research pipeline: event -> labels -> model -> calibrated cohort output | Method diagram |
| Fig. 3 | Reliability curves trước/sau calibration | Held-out predictions |
| Fig. 4 | Spatial hotspot vs teacher region label | Approved page overlays |
| Fig. 5 | Performance/generalization qua course | Outer folds |

Không dùng screenshot dashboard làm methodology figure chính.

## 6. Planned tables

| Table | Nội dung |
|---|---|
| T1 | Dataset/course/participant/window/label statistics |
| T2 | Main baseline comparison với 95% CI |
| T3 | Ablation matrix |
| T4 | Calibration, workload và false-alert tradeoff |
| T5 | Error categories và subgroup coverage |

## 7. Abstract template - chưa điền số

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

Không điền placeholder bằng estimated/fake result.

## 8. Claim-evidence map

| Claim | Evidence bắt buộc | Fallback wording |
|---|---|---|
| Better detection | Preregistered primary metric + CI | “Comparable performance with richer evidence...” |
| Better calibration | Brier/ECE/reliability + CI | “Calibration remains unresolved...” |
| Spatial value | `-spatial` ablation + localization | “Spatial traces provide qualitative anchors...” |
| Generalization | Leave-one-course-out | “Internal validation only...” |
| Learning relevance | Quiz/exam linkage | “Associated with contemporaneous labels...” |
| Actionability | Blinded teacher review | “Designed for teacher review...” |

## 9. Reviewer-style rejection risks

1. **Heuristic dressed as science:** defend bằng learned baselines, ablation và clear implemented/proposed split.
2. **No construct validity:** defend bằng multi-source labels, productive-struggle analysis và teacher reliability.
3. **Data leakage:** publish split logic và immutable manifests.
4. **One-course overclaim:** scope claims hoặc collect multi-course.
5. **Tiny effective sample:** report clustered N/power, không raw event count.
6. **Surveillance concern:** consent, data minimization, aggregate output và student agency.
7. **No educational impact:** không claim impact; position intervention là future work.
8. **Model complexity unnecessary:** strong XGBoost/logistic baselines; accept simpler winner.

## 10. Venue strategy

- Primary community: LAK/EDM/JEDM, venue cụ thể chốt sau pilot và professor review.
- Không ép timeline sáu tuần vào conference deadline.
- Nếu evidence chỉ là system/protocol: workshop/poster/demo hoặc continue study, không hạ standard full paper.
- Nếu multi-course empirical evidence và construct validity mạnh: full research paper.
- Nếu model novelty yếu nhưng dataset/protocol mạnh: artifact/dataset-oriented positioning.

## 11. Reproducibility appendix

- Data card và consent/governance summary.
- Feature/event schema.
- Split manifests và leakage tests.
- Hyperparameter search space, seeds và compute.
- Per-fold metrics/predictions ở mức được phép.
- Calibration implementation.
- Error taxonomy and annotation guide.
- Model card và limitations.

## 12. Internal adversarial review gate

Đây là audit bắt buộc trước khi chuyển từ research specification sang paper draft.

| Trục phản biện | Trạng thái hiện tại | Điều kiện đạt gate |
|---|---|---|
| Contribution/novelty | `PROPOSED`; đã giới hạn novelty boundary | Literature matrix được mentor rà soát, mỗi contribution map tới một result và một closest baseline |
| Construct/method soundness | Công thức production có trace; model nghiên cứu chưa triển khai | Event contract, label provenance, missing-label loss, calibration và leakage tests chạy tái lập được |
| Experimental strength | Protocol đã có; chưa có approved empirical result | B0-B6/M1, ablations, ít nhất ba seeds, course holdout hoặc scope lại thành internal validation |
| Evaluation/statistics | Metric, CI và split đã đặc tả | AUPRC primary, Brier/ECE, cluster bootstrap, effective N, reliability/error/subgroup analysis có artifact |
| Clarity/reproducibility | Dossier song ngữ và claim registry đã có | Introduction không hứa hơn Results; method, manifests, configs, seeds và failures đủ để independent audit |
| Ethics/usefulness | Protocol-first; chưa có institutional approval | Consent, withdrawal, identity separation, teacher actionability và alert workload được phê duyệt/ghi nhận |

**Quy tắc quyết định:**

- Chỉ claim “better detection” khi primary metric và confidence interval vượt gate đã đăng ký trước.
- Chỉ claim “better calibrated” khi Brier/ECE/reliability cùng hỗ trợ kết luận.
- Không claim cross-course generalization nếu không có course-level holdout.
- Không claim improved learning nếu chưa có intervention hoặc assessment linkage phù hợp.
- Negative result vẫn được giữ và dùng để thu hẹp contribution; không thay metric sau khi xem test set.

Trước khi gửi professor, reviewer nội bộ phải xác nhận: mỗi contribution map tới figure/table/result; mỗi major claim có status trong registry; Related Work bao gồm closest prior methods; Method đủ chi tiết để tái lập; experiment lưu cả failure/negative result; và ethics được mô tả ở mức phương pháp, không phải một đoạn disclaimer chung.
