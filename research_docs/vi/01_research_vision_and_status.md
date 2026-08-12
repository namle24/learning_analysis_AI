# Tầm nhìn nghiên cứu và hiện trạng EduPulse

## 1. Mục đích tài liệu

Tài liệu này định vị EduPulse như một **research platform** cho Learning Analytics, không phải bằng chứng rằng sản phẩm hiện tại đã có novelty khoa học. Mục tiêu dài hạn là nghiên cứu cách suy luận điểm nghẽn nhận thức từ hành vi học trên tài liệu số, đồng thời bảo vệ quyền riêng tư và tránh biến telemetry thành công cụ giám sát sinh viên.

Working title của Paper 1:

> **Human-Calibrated Multimodal Cognitive Bottleneck Detection from Learning Micro-Interactions**

Đơn vị phân tích chính không phải “sinh viên X đang bối rối”, mà là **bằng chứng về bottleneck tại một trang/vùng kiến thức trong một cohort và khoảng thời gian xác định**.

## 2. Từ sản phẩm đến research contribution

| Lớp | EduPulse hiện có | Giá trị kỹ thuật | Còn thiếu để thành nghiên cứu |
|---|---|---|---|
| Thu thập | Dwell, scroll reversal, hover, selection, note, annotation, Ask AI, feedback, geometry | Telemetry đa nguồn trong luồng học thật | Consent, schema version, provenance, missingness và data-quality report |
| Phân tích | Page score, coordinate heatmap, sentiment/ABSA, clustering | Baseline giải thích được và triển khai được | Construct validity, learned model, uncertainty, external labels |
| Calibration | Popup xác nhận và attenuation profile | Có vòng lặp false-positive ở mức sản phẩm | Đánh giá held-out, calibration curve, selection-bias analysis |
| Outcome | Flashcard/quiz generation và adaptive mock | Có nền UI cho action loop | Chưa có assessment-attempt pipeline research-ready và mapping item-topic-page |
| Can thiệp | Teaching action/AI insight | Giảng viên nhận khuyến nghị | Chưa có causal study chứng minh cải thiện learning outcome |
| Privacy | RBAC, redaction, pseudonymous aggregate, signed stream | Nền governance tốt | Protocol nghiên cứu, retention, withdrawal, disclosure-risk review |

Kết luận: contribution tiềm năng không nằm ở việc “có dashboard”, mà ở một phương pháp **sensor-free, spatial, cohort-aware, time-aware và human-calibrated**, được kiểm chứng bằng nhiều nguồn ground truth.

## 3. Những gì đã triển khai

### 3.1. Telemetry và micro-interactions - `IMPLEMENTED`

- Page/material/course/session context.
- Active dwell và idle/anomalous dwell flags.
- Scroll reversal, scroll speed, hover count và text-selection count.
- Selection geometry chuẩn hóa trong miền `[0,1]`.
- Text note, highlight, scribble, lasso/visual crop và Ask AI.
- Evidence breakdown, signal kind, confidence heuristic và behavioral flags.

### 3.2. Confusion analytics - `IMPLEMENTED`

- Page/session score kết hợp implicit và explicit evidence.
- Idle decay và attenuation sau false-positive confirmation.
- Dynamic text-note weighting để tách positive engagement khỏi confusion.
- Coordinate heatmap có action depth, time decay, unique actor ratio và logarithmic damping.
- Trend endpoint sử dụng cùng calibrated intensity theo ngày.

### 3.3. Ground-truth loop - `IMPLEMENTED`, scientific impact chưa `VALIDATED`

- Popup xuất hiện khi local score vượt ngưỡng.
- Sinh viên có thể xác nhận true positive hoặc false positive.
- False positive hạ score cục bộ và tạo attenuation profile.
- Bản ghi validation được lưu theo user, course, material, page và thời gian.

### 3.4. Engineering evidence - `VALIDATED` trong phạm vi kỹ thuật

Repo có unit/integration tests cho confusion scoring, coordinate heatmap, validation, telemetry, privacy, RAG và API. Các test này chứng minh code thực hiện đúng contract, không chứng minh mô hình đo đúng trạng thái nhận thức ngoài thực tế.

## 4. Khoảng trống khoa học

### 4.1. Construct gap

“Confusion” là latent construct. Dwell lâu có thể do đọc kỹ, rời máy, nghe giảng hoặc nội dung phức tạp. Note và highlight có thể thể hiện engagement tích cực. Paper phải định nghĩa rõ:

- **Productive struggle:** khó nhưng dẫn tới xử lý sâu và outcome tốt.
- **Unresolved bottleneck:** khó kéo dài, lặp lại hoặc dẫn tới help-seeking/outcome kém.
- **Engagement anchor:** tương tác chủ động nhưng không phải dấu hiệu khó hiểu.
- **Noise:** idle, accidental selection, spam hoặc event thiếu context.

### 4.2. Label gap

Self-report, teacher label, quiz và exam không đo cùng một biến:

- Self-report gần thời điểm nhưng dễ bị response bias.
- Teacher label có ý nghĩa sư phạm nhưng ở mức cohort/page/region.
- Quiz đo near-term knowledge gap và phụ thuộc chất lượng item.
- Exam là delayed outcome, chịu nhiều confounder và không định vị chính xác thời điểm bottleneck.

Không được gộp các nguồn này thành một cột `ground_truth` duy nhất.

### 4.3. Modeling gap

Production score dùng trọng số thủ công và aggregate theo cửa sổ. Nó chưa học temporal sequence, chưa ước lượng uncertainty theo phân phối, chưa kiểm tra generalization qua course và chưa được calibrated trên nhãn thực.

### 4.4. Evaluation gap

Chưa có:

- Grouped/time-aware research split.
- Baseline comparison và ablation đầy đủ.
- Calibration metrics và confidence intervals.
- Teacher annotation reliability.
- Quiz/exam linkage.
- External course validation.

### 4.5. Governance gap

Tài khoản sản phẩm hoặc log production không đồng nghĩa với consent nghiên cứu. Trước khi phân tích để công bố cần approval, participant notice, opt-out/withdrawal, retention và access policy.

## 5. Research program nhiều giai đoạn

| Giai đoạn | Câu hỏi chính | Artifact | Claim cho phép |
|---|---|---|---|
| Paper 1 | Có phát hiện bottleneck tốt hơn bằng micro-interactions và human calibration không? | Method, approved dataset features, benchmark, ablation | Detection/calibration/construct validity |
| Paper 2 | Instructor action dựa trên hotspot có cải thiện learning outcome không? | Prospective intervention hoặc stepped-wedge study | Pedagogical impact/causal evidence |
| Paper 3 | Mô hình có generalize qua môn/trường và thích ứng theo context không? | Multi-institution/domain adaptation study | Robustness/generalization |

Paper 1 không claim hiệu quả can thiệp nếu chưa chạy Paper 2.

## 6. Tiêu chuẩn thành công sau sáu tuần

1. Có bộ protocol song ngữ, paper skeleton và claim registry.
2. Mọi dữ liệu dự kiến thu có data owner, mục đích, retention và label provenance.
3. Có synthetic replay từ event tới feature, model và metric.
4. Current heuristic chạy được như frozen baseline.
5. Proposed prototype có interface, loss, split và evaluation contract cố định.
6. Không có claim nào chuyển từ `PROPOSED` sang `VALIDATED` nếu thiếu evidence.
7. Professor/mentor có thể đưa ra quyết định go/no-go mà không phải suy đoán phần còn thiếu.

## 7. Rủi ro lớn nhất

| Rủi ro | Hậu quả | Giảm thiểu |
|---|---|---|
| Consent bias | Mẫu tham gia không đại diện | So sánh aggregate opt-in/opt-out khi được phép; báo cáo selection process |
| Label sparsity | Model học self-report của nhóm hay phản hồi | Multi-task labels, active sampling, class weighting, prevalence report |
| Leakage | Cùng sinh viên/slide xuất hiện ở train và test | Group split theo student/course/material và temporal cutoff |
| Pseudoreplication | Hàng nghìn event tạo cảm giác sample lớn giả | Cluster-aware bootstrap và mixed-effects model |
| Productive struggle bị gắn nhãn xấu | Khuyến nghị can thiệp sai | Outcome linkage và engagement-vs-bottleneck head |
| Một course duy nhất | Không chứng minh generalization | Leave-one-course-out khi đủ 3-5 course |
| Privacy encroachment | Mất trust và không thể công bố | Data minimization, aggregate output, ethics gate trước collection |

## 8. Quy tắc báo cáo tiến độ

Mỗi tuần cập nhật bốn cột:

| Artifact | Status | Evidence | Blocker |
|---|---|---|---|
| Ví dụ: data dictionary v1 | Implemented | Link file + review log | Chờ ethics owner |

Không dùng phần trăm tiến độ chung. Mỗi artifact phải có acceptance criterion kiểm tra được.
