# Protocol dữ liệu, ground truth và ethics

## 1. Trạng thái và nguyên tắc

Toàn bộ schema/study trong tài liệu này là `PROPOSED` cho research track. Log vận hành hiện có không được tự động chuyển thành research dataset.

Nguyên tắc:

1. Purpose limitation: mỗi field phải gắn với RQ hoặc safety/operations rõ ràng.
2. Data minimization: không thu field chỉ vì “có thể hữu ích sau này”.
3. Separation: PII/account data tách khỏi research features.
4. Provenance: mọi event/label có source, schema version và timestamp.
5. Withdrawal: có cơ chế loại dữ liệu nghiên cứu theo participant key.
6. Aggregate reporting: không công bố hoặc hiển thị đánh giá cá nhân cho giảng viên.

## 2. Đơn vị dữ liệu

| Unit | Khóa logic | Mục đích |
|---|---|---|
| Participant | `research_participant_id` | Pseudonymous linkage trong study |
| Session | participant + material + start time | Nhóm hành vi trong một lần học |
| Event | immutable `event_id` | Tương tác nguyên tử |
| Window | participant + page + time range | Input chính cho model |
| Region | material + page + normalized bbox/grid | Localization và cohort convergence |
| Label | target + source + granularity | Ground-truth observation |
| Assessment outcome | item + participant + attempt | Near/delayed learning outcome |
| Intervention | course/page/action/time | Dành cho future causal study |

## 3. Research event contract

```json
{
  "schema_version": "research-event-v1",
  "event_id": "uuid",
  "research_participant_id": "rotating-pseudonym",
  "consent_version": "consent-v1",
  "course_key": "pseudonymous-course",
  "material_key": "stable-material-version",
  "page_number": 3,
  "event_type": "CREATE_HIGHLIGHT",
  "event_time_utc": "ISO-8601",
  "session_id": "uuid",
  "geometry": {"x": 0.1, "y": 0.2, "width": 0.3, "height": 0.04},
  "behavior": {
    "active_dwell_seconds": 42,
    "scroll_reversals": 2,
    "hover_count": 4,
    "is_idle": false
  },
  "text_features": {
    "has_text": true,
    "sanitized_embedding_ref": "feature-row-id",
    "sentiment_label": "neutral",
    "question_intent": false
  },
  "context": {
    "client_version": "git-sha",
    "content_version": "hash",
    "viewport_bucket": "desktop-medium"
  }
}
```

Không đưa email, student ID, IP đầy đủ, device fingerprint, raw access token hoặc raw note vào research feature table.

## 4. Event taxonomy

| Family | Events | Interpretation boundary |
|---|---|---|
| Passive | `PAGE_VIEW`, active dwell, scroll | Weak evidence; có thể là reading hoặc idle |
| Attention | `TEXT_SELECTION`, hover, revisit | Local attention; chưa đủ kết luận confusion |
| Active | `CREATE_HIGHLIGHT`, `DRAW_SCRIBBLE`, lasso | Cognitive anchor hoặc engagement |
| Constructive | `CREATE_TEXT_NOTE`, self-explanation | Nội dung semantic quyết định confusion/engagement |
| Help-seeking | contextual Ask AI, direct chat | Strong explicit evidence nhưng có thể là curiosity |
| Feedback | difficulty tag, anonymous feedback | Explicit perception; cần quality/sentiment checks |
| Assessment | quiz/exam attempt | Outcome, không phải momentary state |

Mọi alias từ product phải map vào canonical event type và lưu cả `raw_event_type` để audit.

## 5. Ground-truth schema

```json
{
  "label_id": "uuid",
  "research_participant_id": "nullable-for-cohort-label",
  "course_key": "...",
  "material_key": "...",
  "page_number": 3,
  "region": null,
  "label_source": "SELF_REPORT|TEACHER|QUIZ|EXAM",
  "target": "momentary_difficulty|cohort_bottleneck|knowledge_gap",
  "value": 1,
  "scale": "binary|ordinal|continuous",
  "captured_at": "ISO-8601",
  "reference_window_start": "ISO-8601",
  "reference_window_end": "ISO-8601",
  "instrument_version": "...",
  "rater_id": "pseudonymous-or-null",
  "confidence": "optional-rater-confidence"
}
```

Các nguồn label nằm ở các task/head riêng. Không majority-vote self-report, teacher và exam thành một nhãn.

## 6. Self-report sampling để tránh verification bias

Current popup chủ yếu xuất hiện khi score cao. Nếu chỉ dùng popup đó làm label, training set sẽ thiếu negative/low-score windows.

Research protocol dùng stratified experience sampling:

- Chia heuristic score thành low `[0,0.35)`, medium `[0.35,0.75)` và high `[0.75,1]`.
- Sampling window từ cả ba strata; oversample medium/high nhưng giữ inverse-probability weight.
- Tối đa hai research prompts trong một 45-minute session.
- Hai prompt cách nhau ít nhất 10 phút.
- Không prompt trong 60 giây đầu của session hoặc ngay khi đang nhập note/chat.
- Lưu sampling probability và reason (`random_stratum`, `high_trigger`, `control`).
- Câu hỏi tách difficulty và engagement, ví dụ: mức khó hiểu, mức tự tin, đang đọc kỹ hay bị mắc kẹt.

Tỷ lệ sampling cụ thể được điều chỉnh sau usability pilot nhưng phải freeze trước collection chính.

## 7. Teacher annotation protocol

### Unit

Giảng viên gán nhãn page hoặc region trong một material version:

- `NO_BOTTLENECK`
- `POSSIBLE_BOTTLENECK`
- `CONFIRMED_BOTTLENECK`
- `INSUFFICIENT_EVIDENCE`

Kèm category: prerequisite, notation, concept, example, slide density, assignment ambiguity hoặc other.

### Blinding

- Round A: teacher xem content và anonymized student evidence, không xem model score.
- Round B: sau khi khóa label, teacher được xem model output để đánh giá actionability.
- Không sửa Round A label sau khi xem prediction; nếu có reconsideration, lưu label mới với reason.

### Reliability

- Ít nhất 20% sampled pages/regions có hai raters độc lập nếu nguồn lực cho phép.
- Báo cáo Cohen's kappa cho binary/nominal và weighted kappa cho ordinal labels.
- Bất đồng dùng adjudication label nhưng vẫn giữ raw rater labels.

## 8. Quiz và exam linkage

### Assessment item map

Trước khi thu outcome, instructor/researcher map mỗi item tới:

- course/topic/learning objective.
- material version và page/region liên quan.
- cognitive level và item difficulty dự kiến.
- thời điểm item được mở so với telemetry window.

### Outcomes

- Quiz: first attempt correctness, attempts, latency và confidence nếu có.
- Exam: item-level correctness nếu policy cho phép; không chỉ dùng tổng điểm môn.
- Giữ item version để tránh trộn câu đã sửa.
- Không đưa outcome xảy ra trước input window vào target tương lai.

Quiz generation hiện có trong product không đủ làm validated assessment. Item phải qua instructor review và quality check.

## 9. Consent và participant communication

Consent/notice phải nói rõ:

- Dữ liệu nào được thu và mục đích nào.
- Tính năng học tập vẫn dùng được ra sao nếu không tham gia research.
- Ai truy cập identifiable linkage và ai chỉ truy cập de-identified data.
- Thời gian lưu, địa điểm lưu và quy trình xóa/withdrawal.
- Dữ liệu có được gửi tới external AI provider hay không.
- Kết quả chỉ báo cáo aggregate; không ảnh hưởng điểm học tập.
- Liên hệ researcher, supervisor và ethics contact.

Không dùng dark pattern hoặc gộp research consent với điều khoản bắt buộc để truy cập môn học.

## 10. Privacy architecture

```text
Identity store
  email/student code -> internal user ID
          |
          | restricted linkage service
          v
Research linkage vault
  internal user ID -> rotating research participant ID
          |
          v
Research feature store
  no direct identifiers, sanitized derived features
```

- Linkage vault có quyền truy cập riêng và audit log.
- Pseudonym rotation theo study/course nếu longitudinal design không yêu cầu global ID.
- Raw text được sanitize trước feature extraction; raw private note không release.
- IP/device security logs không đưa vào learning model mặc định.
- Public artifact chỉ gồm de-identified features sau disclosure-risk review.

## 11. Retention và withdrawal

Đề xuất để ethics review chốt:

| Data | Working retention | Withdrawal action |
|---|---|---|
| Consent record | Theo institutional policy | Giữ audit tối thiểu nếu bắt buộc pháp lý |
| Identity linkage | Tới khi kết thúc verification + grace period | Xóa mapping và queued research rows |
| Raw approved events | Ngắn nhất cần cho feature QA | Xóa theo participant key |
| Derived features | Theo approved study duration | Xóa hoặc tombstone trước final freeze |
| Aggregate published statistics | Không thể rút cá nhân sau publication | Giải thích rõ trong consent |

Không hard-code thời gian pháp lý khi chưa có institutional decision.

## 12. Data-quality gates

Trước training, report tối thiểu:

- Event count theo type/course/material/client version.
- Unique participants và sessions; không dùng raw events làm sample size headline.
- Missingness theo field và label source.
- Duplicate/idempotency rate.
- Timestamp ordering và clock skew.
- Geometry out-of-range/zero-area rate.
- Idle/dwell anomaly rate.
- Consent and withdrawal reconciliation.
- Label prevalence theo sampling stratum.
- Participant contribution distribution và top-contributor cap analysis.

Go/no-go nếu có schema drift không giải thích, missing label provenance, consent mismatch hoặc leakage giữa identity/research stores.

## 13. Dataset release policy

Mặc định release sau approval:

- Feature-level de-identified tables.
- Synthetic fixtures và schema.
- Split manifests không chứa identifier gốc.
- Data card, datasheet, known biases và access license.
- Code để tái tạo metrics.

Không release mặc định:

- Raw note/feedback text.
- Email, student code, IP, exact device fingerprint.
- Original private annotations có thể chứa handwriting/PII.
- Small-cell subgroup aggregates có nguy cơ re-identification.

## 14. Data access roles

| Role | Quyền |
|---|---|
| Identity custodian | Linkage/withdrawal, không train model |
| Data engineer | Approved pseudonymous events, không xem PII |
| Research analyst | Frozen feature set và labels |
| Instructor rater | Material/evidence được phân công, không xem identity |
| External reviewer | Aggregate artifacts hoặc controlled-access dataset |

Mọi export có purpose, owner, timestamp và checksum.
