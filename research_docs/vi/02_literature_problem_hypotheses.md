# Literature, bài toán và giả thuyết nghiên cứu

## 1. Trạng thái của literature review

Đây là **scoping review seed**, chưa phải systematic review hoàn tất. Danh sách ban đầu nằm tại [literature_matrix.csv](../literature_matrix.csv). Trước khi viết Related Work chính thức, team phải chạy protocol tìm kiếm có ngày chốt, database, query, inclusion/exclusion và quy trình screening.

## 2. Nền lý thuyết

### 2.1. Confusion không luôn luôn tiêu cực

Nghiên cứu về cognitive-affective dynamics chỉ ra confusion có thể đóng vai trò xây dựng nếu được giải quyết, nhưng có thể chuyển thành frustration hoặc disengagement nếu kéo dài. Vì vậy EduPulse không dự đoán “bad state” đơn giản; Paper 1 nhắm tới **unresolved cognitive bottleneck** và phải phân biệt productive struggle.

### 2.2. Hành vi quan sát được không đồng nhất với trạng thái nhận thức

ICAP phân biệt Passive, Active, Constructive và Interactive engagement từ hành vi học. Note, highlight hoặc Ask AI thể hiện mức độ chủ động khác nhau, nhưng hành động chủ động không tự động đồng nghĩa với confusion. Đây là lý do cần engagement head, semantic filter và downstream outcome.

### 2.3. Sensor-free affect detection đã có lịch sử nghiên cứu

Các nghiên cứu trước đã dùng clickstream, forum language và fine-grained logs để dự đoán confusion/affect. Do đó novelty của EduPulse không thể là “kết hợp hành vi và văn bản”. Điểm cần kiểm chứng là tổ hợp mới:

- Region-level spatial anchors trên tài liệu thật.
- Micro-interaction sequence thay vì aggregate click count.
- Cohort convergence tại cùng vùng kiến thức.
- Human calibration theo false-positive feedback.
- Multi-source outcomes giữ nguyên provenance.
- Privacy-first deployment trong lớp học thật.

### 2.4. Calibration là yêu cầu, không phải trang trí

Trong bối cảnh giảng viên ra quyết định, xác suất 0.8 phải có ý nghĩa gần với tỷ lệ đúng thực tế. Vì vậy Paper 1 báo cáo Brier/ECE và reliability curve, không chỉ AUROC/F1. Threshold production không được chọn trên test set.

### 2.5. Ethics và learner agency

Multimodal Learning Analytics có rủi ro chuyển từ hỗ trợ sang encroachment. Consent, data minimization, access boundary và khả năng giải thích/kháng nghị phải thuộc phương pháp nghiên cứu, không đặt ở phụ lục sau cùng.

## 3. Problem statement

Cho một course có tập sinh viên `S`, material `M`, page/region `R` và chuỗi event theo thời gian `E`, mục tiêu là ước lượng bằng chứng bottleneck ở hai mức:

1. `p_individual`: xác suất một student-page window chứa unresolved difficulty evidence.
2. `p_cohort`: xác suất một page/region là bottleneck đáng chú ý ở cấp cohort.

Mô hình phải:

- Phân biệt engagement khỏi confusion.
- Tận dụng temporal order, spatial overlap và content context.
- Đưa ra uncertainty/calibrated probability.
- Generalize qua student/material/course.
- Không cần camera, microphone hoặc biometric sensors.
- Không hiển thị student-level judgment cho giảng viên ngoài protocol được duyệt.

## 4. Research questions

### RQ1 - Incremental validity

Micro-interactions có tăng chất lượng phát hiện bottleneck so với macro telemetry như dwell/page view không?

### RQ2 - Human calibration

Self-report false-positive calibration và multi-source supervision có cải thiện probability calibration và giảm false alert mà không làm mất recall quan trọng không?

### RQ3 - Spatial-cohort validity

Sự hội tụ của nhiều sinh viên tại cùng page/region có dự đoán teacher-confirmed bottleneck và quiz/exam error tốt hơn raw interaction count không?

### RQ4 - Deferred

Khuyến nghị dựa trên bottleneck có cải thiện outcome không? Câu hỏi này dành cho intervention study sau Paper 1.

## 5. Giả thuyết preregistration

| ID | Giả thuyết | So sánh | Metric chính | Điều kiện bác bỏ |
|---|---|---|---|---|
| H1 | Multimodal model tốt hơn dwell-only | Proposed vs dwell-only | AUPRC | CI của chênh lệch chứa 0 hoặc effect dưới minimum-relevant delta đã preregister |
| H2 | Micro-interactions có incremental value | Full vs bỏ micro-interactions | AUPRC, Brier | Không cải thiện cả discrimination lẫn calibration |
| H3 | Human calibration giảm false alerts | Calibrated vs uncalibrated | FPR tại recall cố định, ECE | FPR không giảm hoặc recall giảm quá tolerance preregister |
| H4 | Unique-user spatial aggregation tốt hơn raw count | Cohort-spatial vs count baseline | Region AUPRC/IoU | Không có cải thiện ngoài sampling error |
| H5 | Tín hiệu dự đoán outcome gần tốt hơn outcome xa | Quiz vs exam head | AUPRC | Không quan sát gradient theo temporal proximity |
| H6 | Model giữ hiệu năng qua course | Leave-one-course-out | Relative AUPRC drop | Drop vượt generalization tolerance preregister |

Các giá trị minimum-relevant delta và tolerance chỉ được khóa sau pilot prevalence/power analysis, trước final test.

## 6. Novelty claim được phép

Nếu evidence đầy đủ, Paper 1 có thể claim:

1. Một problem formulation cho cohort cognitive bottleneck từ micro-interaction trên tài liệu số.
2. Một multi-task model giữ riêng các nguồn nhãn và kết hợp temporal-spatial context.
3. Một human calibration loop được đánh giá bằng calibration và false-alert metrics.
4. Một prospective dataset/protocol privacy-aware trong lớp học thật.

Không được claim:

- “Mô hình đọc được suy nghĩ” hoặc chẩn đoán cảm xúc.
- “Dwell time chứng minh sinh viên không hiểu”.
- “Top-tier novelty” trước literature audit và experiment.
- “Cải thiện kết quả học” nếu chưa có intervention study.
- “Generalize toàn giáo dục” từ một course hoặc một trường.

## 7. Protocol tìm kiếm literature

### Database

- ACM Digital Library.
- Scopus hoặc Web of Science nếu trường có quyền truy cập.
- ERIC.
- IEEE Xplore.
- SpringerLink và ScienceDirect cho AIED/education journals.
- Proceedings chính thức LAK, EDM và AIED.

### Query groups

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

### Inclusion

- Peer-reviewed study có method/data rõ.
- Hành vi trong digital learning hoặc classroom learning.
- Có label/outcome, evaluation hoặc theoretical construct liên quan.
- English; từ 2010 tới ngày khóa search, cộng foundational work trước 2010 nếu cần.

### Exclusion

- Chỉ mô tả dashboard không có evaluation.
- Marketing/blog không có phương pháp.
- Affect detection chỉ dùng biometric sensor mà không có transferable method.
- Không phân biệt prediction target hoặc không mô tả label provenance.

### Screening output

Hai reviewer độc lập screen title/abstract cho tập chính. Bất đồng được resolve bằng thảo luận; lưu lý do exclude ở full-text stage. Related Work chỉ gọi là systematic nếu protocol và flow được hoàn thành.

## 8. Conceptual framework

```text
Learning context
  -> observable micro-interactions
  -> latent processing state
  -> self-report / teacher interpretation / assessment outcome

Observable interaction != latent state != learning outcome
```

Mô hình dự đoán các observation tasks liên quan tới latent state; không giả định bất kỳ một observation nào là ground truth hoàn hảo.
