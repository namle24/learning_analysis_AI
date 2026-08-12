# Phương pháp hiện tại và mô hình đề xuất

## 1. Nguyên tắc versioning

Tài liệu tách hai hệ thống:

- **Production heuristic v1 - `IMPLEMENTED`:** công thức đang chạy trong EduPulse.
- **Research model v0 - `PROPOSED`:** prototype cho Paper 1, chưa được xem là tốt hơn cho tới khi benchmark hoàn tất.

Không được thay công thức production bằng research model trong thời gian thu thập mà không version event/model và ghi mốc rollout.

## 2. Production page/session score

### 2.1. Chuẩn hóa tín hiệu

Với threshold đọc trang `T` lấy từ page metadata hoặc fallback `180` giây:

```text
dwell_raw = min(dwell_seconds / T, 1)
scroll = min(scroll_reversals / 6, 1)
selection = min(text_selection_count / 4, 1)
hover = min(hover_count / 12, 1)
```

Nếu `is_idle=true` và dwell đạt ít nhất `120` giây:

```text
dwell = dwell_raw * 0.1
```

Idle-only session còn bị cap để không tạo strong evidence. False-positive profile áp attenuation `a` trong `[0,1]` lên implicit components.

Explicit counts hiện được nhị phân hóa thành `0/1` để hạn chế spam trong một payload:

```text
contextual_ai, direct_chat, negative_feedback, annotation
```

### 2.2. Công thức đang chạy

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

Các trọng số lấy từ environment/config và phải được log cùng model/config version trong nghiên cứu.

### 2.3. Text-note routing

Typed note mặc định có action weight `2.5` trong heatmap. Nếu sentiment/label hoặc conservative keyword rules cho thấy note tích cực/review và không có question/stuck cue, confusion weight hạ xuống `0.2` và event đi vào engagement channel.

Điều này là rule-based mitigation, chưa phải validated multilingual classifier.

### 2.4. Confidence heuristic

Confidence bắt đầu từ `0.18`, tăng theo số channel hoạt động và có điều chỉnh cho direct chat. Nó bị cap khi có idle-only, low-information text hoặc action thiếu reading context. Đây là evidence-quality heuristic, không phải calibrated probability.

## 3. Production coordinate intensity

Với tập event trong một grid cell hoặc page/day:

```text
I = alpha * (U / N_safe) * ln(1 + sum_i(w_i * exp(-lambda * age_i)))
```

Trong đó:

- `U`: số actor pseudonymous duy nhất.
- `N_safe = max(class_size, U, 1)`; fallback class size là `400` nếu không có enrollment.
- `lambda = 0.1` theo ngày.
- `alpha`: trung bình implicit attenuation profile active theo material; fallback `1.0`.
- `ln(1 + ...)`: logarithmic damping chống repeated-event inflation.

Action weights hiện tại:

| Action | Weight |
|---|---:|
| AI question / chat engagement | 3.0 |
| Create text note | 2.5 hoặc 0.2 nếu positive engagement |
| Flashcard fail | 2.0 |
| Draw/scribble | 1.8 |
| Visual lasso / note crop | 1.5 |
| Create highlight | 1.2 |
| Dwell spike / page view | 1.0 |
| Text selection | 0.7 |
| Fallback telemetry | 0.5 |

Text selection/highlight bounds được sample thành các điểm trên vùng với giới hạn số mẫu để tránh geometry lớn gây bùng chi phí.

### Scientific limitation

`alpha`, `lambda` và `w_i` hiện là design choices. Paper 1 phải xem chúng là baseline hyperparameters, chạy sensitivity analysis và so sánh với learned parameters. Không mô tả chúng là “cognitive constants”.

## 4. Proposed research model

### 4.1. Input window

Đơn vị input là student-page window có độ dài tối đa `K` event trong khoảng thời gian preregister. Mỗi event gồm:

```text
categorical: event_type, source, device_class, page/material/course
continuous: active_dwell, reversals, speed, hover, x/y/w/h, age
binary: idle, anomalous, explicit_action, has_text
semantic: sanitized text embedding, sentiment/intent labels
content: page token density, visual density, formula/table indicators
provenance: schema_version, client_version, model/prompt version
```

Raw PII và raw private note không đi vào release artifact.

### 4.2. Architecture v0

1. **Event encoder:** embeddings cho categorical features; normalized MLP cho continuous features; frozen existing text embedding cho sanitized text.
2. **Student-page sequence encoder:** một GRU một chiều để giữ thứ tự event và tránh model quá lớn trong prototype sáu tuần.
3. **Spatial encoder:** MLP trên normalized bbox cộng region density features.
4. **Cohort aggregator:** permutation-invariant DeepSets trên student-page representations trong cùng page/region/time window.
5. **Multi-task heads:** self-report difficulty, teacher-confirmed bottleneck, quiz error và delayed exam-risk head.
6. **Engagement head:** positive/constructive interaction để tách productive engagement khỏi unresolved bottleneck.
7. **Calibration:** temperature scaling riêng cho mỗi classification head trên calibration split.

Transformer chỉ là challenger model sau khi GRU baseline ổn định; không mặc định dùng vì sample hiệu dụng có thể nhỏ hơn raw event count rất nhiều.

### 4.3. Multi-task loss

Với task `k`, label có mask `m_ik` vì không phải event nào cũng có đủ nhãn:

```text
L_supervised = sum_k lambda_k * (
  sum_i m_ik * BCE(y_ik, p_ik) / max(sum_i m_ik, 1)
)
```

Thêm regularization:

```text
L = L_supervised
  + beta * L_engagement_separation
  + gamma * L_weight_decay
```

Không dùng test set để chọn `lambda_k`, `beta`, `gamma`, threshold hoặc temperature.

### 4.4. Outputs

```json
{
  "model_version": "research-v0",
  "window_id": "pseudonymous-window-id",
  "probabilities": {
    "self_report_difficulty": 0.0,
    "teacher_bottleneck": 0.0,
    "near_term_quiz_error": 0.0,
    "delayed_exam_risk": 0.0,
    "constructive_engagement": 0.0
  },
  "uncertainty": {
    "method": "temperature_scaling",
    "calibration_set_version": "..."
  },
  "evidence_summary": {
    "top_modalities": [],
    "unique_students": 0,
    "sample_size_warning": true
  }
}
```

Instructor output chỉ hiển thị cohort/page/region aggregate và sample-size warning.

## 5. Model comparison contract

| Model | Purpose |
|---|---|
| Dwell-only | Kiểm tra weak-signal baseline |
| Raw count | Kiểm tra lợi ích của chống spam và context |
| Production heuristic | Đo lift so với hệ thống đang chạy |
| Logistic regression | Linear interpretable baseline |
| Gradient-boosted trees | Strong tabular baseline |
| GRU single-task | Giá trị của temporal sequence |
| Proposed multi-task GRU + DeepSets | Giá trị của label separation và cohort-spatial context |

Nếu proposed model không vượt strong tabular baseline với CI đáng tin cậy, contribution phải chuyển sang dataset/protocol/construct finding thay vì tuyên bố model superiority.

## 6. Explainability

Paper 1 dùng:

- Modality ablation là evidence chính.
- Permutation importance/SHAP cho tabular baseline.
- Event/region contribution summary cho proposed model.
- Error case với timeline và geometry đã de-identify.

Không dùng attention weight như bằng chứng nhân quả.

## 7. Reproducibility requirements

- Frozen feature schema và data hash.
- Seed list tối thiểu ba seeds cho learned model.
- Config file lưu split, model, hyperparameters và threshold.
- Environment lock/container.
- Command độc lập cho feature build, train, calibrate và evaluate.
- Output gồm per-fold predictions để bootstrap lại metric.
- Không ghi secret, raw PII hoặc raw private note vào experiment logs.
