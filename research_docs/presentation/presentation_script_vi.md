# Kịch bản thuyết trình nghiên cứu EduPulse

Kịch bản đi kèm: [edupulse_research_beamer_vi.html](./edupulse_research_beamer_vi.html)

**Thời lượng mục tiêu:** 15–18 phút trình bày, 5–10 phút hỏi đáp  
**Đối tượng:** giảng viên hướng dẫn, hội đồng nghiên cứu, nhóm Learning Analytics/EDM  
**Thông điệp xuyên suốt:** EduPulse không cố chẩn đoán trạng thái tâm lý của từng sinh viên. Nghiên cứu tìm kiếm bằng chứng đáng tin cậy về những trang hoặc vùng kiến thức mà nhiều người học có thể đang gặp điểm nghẽn.

## Cách sử dụng

- Mở file HTML bằng trình duyệt.
- Dùng phím `←` và `→` để chuyển slide; `O` để xem tổng quan; `P` để in PDF.
- Không cần đọc toàn bộ chữ trên slide. Dùng slide làm bằng chứng trực quan và trình bày theo kịch bản dưới đây.
- Các slide 22–23 là tài liệu tham khảo, thường không cần trình bày trừ khi được hỏi.
- Các từ `IMPLEMENTED`, `PROPOSED`, `VALIDATED` và `FUTURE` phải được nói đúng nghĩa để tránh overclaim.

---

## Slide 1 — Phát hiện điểm nghẽn nhận thức từ vi tương tác học tập

**Thời lượng:** 35–45 giây

**Lời thoại**

> Xin chào thầy cô và các anh chị. Nghiên cứu của tôi tập trung vào một câu hỏi: trong quá trình sinh viên đọc slide và tài liệu số, liệu những tương tác rất nhỏ như dừng đọc, cuộn ngược, chọn văn bản, ghi chú, đánh dấu hoặc hỏi AI có thể giúp phát hiện sớm những vùng kiến thức mà cả lớp đang gặp khó khăn hay không?
>
> Hướng tiếp cận của EduPulse không sử dụng camera, microphone hay cảm biến sinh trắc. Mục tiêu là xây dựng một phương pháp Learning Analytics dựa trên dấu vết tương tác tự nhiên, có ngữ cảnh không gian, thời gian và cohort, đồng thời được hiệu chuẩn bằng phản hồi của con người.

**Chuyển ý:** Trước hết, tôi xin làm rõ mục đích cuối cùng của nghiên cứu.

## Slide 2 — Mục đích nghiên cứu

**Thời lượng:** 40 giây

**Lời thoại**

> Mục đích không phải là kết luận “sinh viên A đang bối rối”. Mục đích là cung cấp cho giảng viên bằng chứng sớm về vị trí nội dung mà một nhóm người học có thể đang gặp điểm nghẽn.
>
> Nghiên cứu hướng tới ba giá trị. Thứ nhất là nhận biết sớm, trước khi khó khăn chỉ xuất hiện qua bài thi. Thứ hai là hỗ trợ quyết định: giảng viên biết phần nào cần giải thích lại hoặc bổ sung tài liệu. Thứ ba là bảo vệ người học bằng cách ưu tiên báo cáo tổng hợp cấp cohort thay vì giám sát cá nhân.

**Nhấn mạnh:** Đối tượng dự đoán là *bằng chứng bottleneck*, không phải trạng thái tâm lý tuyệt đối.

## Slide 3 — Vì sao bài toán này đáng nghiên cứu?

**Thời lượng:** 45–55 giây

**Lời thoại**

> Trong lớp học số, giảng viên thường mất phần lớn tín hiệu phi ngôn ngữ vốn có trong lớp trực tiếp. Khi nhận ra một chủ đề khó qua quiz hoặc kỳ thi thì có thể đã muộn.
>
> Tuy nhiên, dùng một proxy đơn giản cũng rất nguy hiểm. Một sinh viên dừng lâu có thể đang đọc kỹ, đã rời máy hoặc gặp nội dung phức tạp. Một ghi chú hay highlight có thể là dấu hiệu học tập chủ động chứ không phải confusion.
>
> Vì vậy, nguyên tắc nền tảng là: hành vi quan sát được không đồng nhất với trạng thái nhận thức, và trạng thái nhận thức cũng không đồng nhất với kết quả học tập. Nghiên cứu phải mô hình hóa và kiểm chứng mối liên hệ giữa ba lớp này thay vì giả định chúng giống nhau.

## Slide 4 — Khóa khái niệm trước khi xây mô hình

**Thời lượng:** 45 giây

**Lời thoại**

> Tôi phân biệt bốn khái niệm. Productive struggle là khó khăn có ích, dẫn tới xử lý sâu và cuối cùng được giải quyết. Unresolved bottleneck là khó khăn kéo dài, lặp lại hoặc liên hệ với help-seeking và outcome kém. Engagement anchor là tương tác chủ động như ghi chú hay self-explanation. Cuối cùng là noise, gồm idle, lựa chọn nhầm hoặc spam sự kiện.
>
> Target chính của Paper 1 là unresolved bottleneck. Việc phân biệt này rất quan trọng, vì nếu hệ thống coi mọi nỗ lực học sâu là tín hiệu xấu thì can thiệp có thể phản tác dụng.

**Chuyển ý:** Với định nghĩa đó, chúng ta có thể xác định khoảng trống so với nghiên cứu trước.

## Slide 5 — Nghiên cứu trước đã làm gì, còn thiếu gì?

**Thời lượng:** 60 giây

**Lời thoại**

> Nghiên cứu trước đã chỉ ra ba điều quan trọng. Confusion không luôn tiêu cực. Clickstream, văn bản và log chi tiết đã từng được dùng để dự đoán affect. Và thứ tự hành động thường mang nhiều thông tin hơn count tĩnh.
>
> Vì vậy, novelty của EduPulse không thể chỉ là “kết hợp hành vi và văn bản”. Khoảng trống tôi nhắm tới là tổ hợp của chuỗi micro-interaction, vị trí cụ thể trên tài liệu, sự hội tụ của nhiều sinh viên tại cùng vùng, xác suất được hiệu chuẩn và cơ chế human feedback.
>
> Đồng thời, privacy và consent không được xem như phần disclaimer cuối bài, mà phải là một phần của thiết kế nghiên cứu.

**Lưu ý khi bị hỏi:** Literature matrix hiện là scoping-review seed; novelty cuối cùng chỉ được khóa sau systematic search và closest-work audit.

## Slide 6 — Bài toán nghiên cứu

**Thời lượng:** 75–90 giây

**Lời thoại**

> Bài toán được mô hình hóa ở hai cấp.
>
> Xác suất thứ nhất, `p_individual`, là xác suất một cửa sổ student–page–time chứa bằng chứng về khó khăn chưa được giải quyết. Ví dụ, một sinh viên đọc lại, cuộn ngược, chọn một công thức và đặt câu hỏi về nó. Xác suất này giúp mô hình hiểu chuỗi bằng chứng cục bộ và liên kết với self-report hoặc quiz. Đây là biến trung gian nghiên cứu, không phải nhãn được hiển thị cho giảng viên.
>
> Xác suất thứ hai, `p_cohort`, là xác suất một trang hoặc vùng nội dung là bottleneck đáng chú ý đối với cả nhóm. Nó xem xét số người học khác nhau, mức độ hội tụ tại cùng vị trí, sự lặp lại theo thời gian và context của nội dung. Đây mới là đầu ra chính để tạo hotspot và hỗ trợ giảng viên.
>
> Ví dụ, một sinh viên dừng lâu ở công thức chỉ làm bằng chứng cá nhân tăng nhẹ. Nhưng nếu nhiều sinh viên cùng quay lại, chọn và hỏi về chính công thức đó, bằng chứng cohort tăng mạnh.

**Cách nói ngắn gọn:**

> `p_individual` giúp hiểu tín hiệu cục bộ; `p_cohort` giúp quyết định vùng nào đáng được giảng viên xem xét.

**Lưu ý kỹ thuật:** Labels dùng để huấn luyện và đánh giá, không phải input khi inference. Công thức chính xác hơn cho cohort là:

```text
p_cohort = P(cohort bottleneck = 1 |
             interaction evidence, content, context)
```

**Chuyển ý:** Từ bài toán này, tôi đặt ra ba mục tiêu có thể kiểm chứng.

## Slide 7 — Mục tiêu nghiên cứu có thể kiểm chứng

**Thời lượng:** 45 giây

**Lời thoại**

> Mục tiêu thứ nhất là kiểm tra micro-interactions có cung cấp incremental validity so với dwell và page view hay không. Mục tiêu thứ hai là kiểm tra human calibration có giảm false alert mà vẫn giữ recall quan trọng hay không. Mục tiêu thứ ba là kiểm tra spatial cohort convergence có dự đoán teacher-confirmed bottleneck tốt hơn raw count hay không.
>
> Việc chứng minh khuyến nghị làm tăng kết quả học không thuộc Paper 1. Claim đó cần một intervention study riêng ở giai đoạn sau.

## Slide 8 — Từ câu hỏi nghiên cứu tới kiểm định

**Thời lượng:** 50 giây

**Lời thoại**

> Mỗi research question được gắn với một so sánh có thể bác bỏ. RQ1 so sánh mô hình đầy đủ với dwell-only và ablation bỏ micro-interactions. RQ2 so sánh trước và sau calibration tại cùng mức recall. RQ3 so sánh spatial cohort model với raw count và các ablation bỏ spatial hoặc unique-user aggregation.
>
> Ngoài ra, tôi kiểm tra outcome gần như quiz so với outcome xa như exam, và kiểm tra generalization bằng leave-one-course-out. Minimum effect và tolerance sẽ được preregister sau pilot nhưng trước khi mở final test.

## Slide 9 — Nền tảng đã có không đồng nghĩa đóng góp khoa học

**Thời lượng:** 50 giây

**Lời thoại**

> Repo hiện đã có telemetry, note, annotation, Ask AI, heuristic score, heatmap và vòng lặp false-positive. Đây là nền tảng kỹ thuật quan trọng.
>
> Tuy nhiên, tôi tách rất rõ engineering evidence khỏi scientific evidence. Unit test chứng minh code chạy đúng contract nhưng chưa chứng minh model đo đúng bottleneck ngoài thực tế. Research model, external labels và comparative evaluation hiện vẫn là proposed. Improved learning outcome là future work.

**Nhấn mạnh:** Không gọi heuristic hiện tại là mô hình khoa học đã được xác thực.

## Slide 10 — Từ hành động rời rạc tới chuỗi bằng chứng

**Thời lượng:** 45–55 giây

**Lời thoại**

> Dữ liệu được tổ chức theo mức độ tương tác: passive như dwell và scroll; attention như hover, selection và revisit; active như highlight và drawing; constructive như note; help-seeking như Ask AI.
>
> Nhưng event type là chưa đủ. Mỗi event cần đi kèm thời gian, vị trí chuẩn hóa trên trang, content version, device, idle flag và schema version. Input chính là một chuỗi event trong student–page window.
>
> Số lượng event không được dùng như sample size headline. Phân tích phải dựa trên effective units như participant và course để tránh pseudoreplication.

## Slide 11 — Pipeline nghiên cứu đề xuất

**Thời lượng:** 65 giây

**Lời thoại**

> Pipeline bắt đầu bằng event features, đặc trưng nội dung và đặc trưng ngữ nghĩa. GRU giữ thứ tự tương tác của từng student–page window. Spatial encoder biểu diễn bounding box và mật độ vùng. DeepSets tổng hợp các representation của nhiều sinh viên mà không phụ thuộc thứ tự.
>
> Các prediction head được tách theo self-report, teacher label, quiz, exam và constructive engagement. Masked loss cho phép học khi mỗi mẫu chỉ có một phần nguồn nhãn. Cuối cùng, temperature scaling được thực hiện trên calibration split riêng.
>
> Tôi chọn GRU cho prototype vì effective sample size có thể nhỏ hơn số event rất nhiều. Transformer chỉ là challenger nếu pilot cho thấy dữ liệu đủ lớn.

## Slide 12 — AI/LLM đóng vai trò gì?

**Thời lượng:** 60 giây

**Lời thoại**

> AI và LLM có bốn vai trò. Thứ nhất, hiểu nội dung học liệu: trích xuất khái niệm, learning objective và liên kết slide với quiz. Thứ hai, hiểu ý định của note hoặc câu hỏi, chẳng hạn phân biệt khó hiểu, tò mò, ôn tập và self-explanation.
>
> Thứ ba, LLM hỗ trợ human calibration bằng cách chọn mẫu, tóm tắt evidence và gợi ý label để giáo viên xác nhận. LLM không được tự tạo ground truth. Thứ tư, ở giai đoạn can thiệp, LLM có thể tạo giải thích hoặc câu hỏi chẩn đoán dựa trên evidence và course content.
>
> Tóm lại, LLM là semantic copilot, không phải máy chẩn đoán confusion.

## Slide 13 — Tích hợp LLM như một module có thể kiểm định

**Thời lượng:** 60 giây

**Lời thoại**

> Đầu vào LLM chỉ gồm văn bản đã sanitize và corpus môn học được phê duyệt. Đầu ra là intent, concept và semantic features đưa vào mô hình chính.
>
> Giá trị của LLM phải được kiểm tra bằng ablation `minus LLM semantic`, đồng thời so sánh với TF–IDF, classifier nhỏ và embedding baseline. Tôi cũng đánh giá riêng tiếng Việt, tiếng Anh và code-switching, cùng độ ổn định khi prompt hoặc model version thay đổi.
>
> Các guardrail gồm PII redaction, retrieval từ nguồn môn học, citation về evidence, version log và human approval. Hallucination và data leakage được xem là lỗi phương pháp, không chỉ là lỗi giao diện.

**Nếu được hỏi “vì sao cần LLM?”**

> Chỉ giữ LLM nếu nó tạo incremental value đáng tin cậy. Nếu một classifier nhỏ đạt hiệu quả tương đương và ổn định hơn, nghiên cứu nên chọn giải pháp đơn giản hơn.

## Slide 14 — Không có một cột ground truth duy nhất

**Thời lượng:** 55 giây

**Lời thoại**

> Self-report, teacher label, quiz và exam không đo cùng một biến. Self-report gần thời điểm nhưng có response bias. Teacher label có giá trị sư phạm nhưng ở cấp page hoặc region. Quiz đo knowledge gap gần, còn exam chịu nhiều confounder hơn.
>
> Vì vậy, tôi không gộp các nguồn thành một cột ground truth. Multi-task model giữ nguyên source, granularity và timestamp. Teacher annotation cần double rating trên một phần mẫu và báo inter-rater reliability.

## Slide 15 — Novelty nằm ở tổ hợp nào?

**Thời lượng:** 55 giây

**Lời thoại**

> Novelty dự kiến có ba thành phần. Một là chuỗi micro-interaction được neo vào vùng nội dung cụ thể. Hai là cohort convergence, tức nhiều người học cùng tạo bằng chứng ở một knowledge region, có kiểm soát repeated-event inflation. Ba là multi-source human calibration với calibrated probability và uncertainty.
>
> Định vị ngắn gọn là sensor-free, spatial, cohort-aware, time-aware, human-calibrated và privacy-first. Đây vẫn là novelty hypothesis; nó chỉ trở thành contribution sau literature audit và ablation.

## Slide 16 — Đóng góp dự kiến

**Thời lượng:** 50 giây

**Lời thoại**

> Tôi dự kiến bốn đóng góp. Đóng góp về bài toán và construct; đóng góp phương pháp temporal–spatial multi-task; đóng góp thực nghiệm prospective trên nhiều course; và đóng góp artifact gồm schema, protocol, code và dữ liệu feature-level nếu được phép.
>
> Mỗi contribution có evidence gate. Nếu chỉ có một course, tôi sẽ gọi kết quả là internal validation. Nếu model không hơn boosted trees, contribution sẽ chuyển sang construct, protocol hoặc dataset finding thay vì tiếp tục tuyên bố model superiority.

## Slide 17 — Thiết kế đánh giá chống leakage và overclaim

**Thời lượng:** 65 giây

**Lời thoại**

> Evaluation trả lời riêng ba câu: model có phân biệt tốt không, xác suất có được calibration tốt không, và prediction có ý nghĩa giáo dục hay không.
>
> AUPRC là metric chính vì positive có thể hiếm. Calibration dùng Brier, ECE và reliability curve. Localization dùng IoU và Recall at K. Giá trị thực tế được đo bằng lead time và false alerts trên một trăm student-hours.
>
> Tất cả model dùng cùng split. Participant được group cùng fold; course được hold out; calibration split tách khỏi test. Confidence interval dùng hierarchical cluster bootstrap thay vì coi mọi event là độc lập.

## Slide 18 — Privacy và learner agency

**Thời lượng:** 50 giây

**Lời thoại**

> Identity store được tách khỏi research feature store qua restricted linkage và rotating pseudonym. Raw private note, IP hay device fingerprint không được đưa vào research features mặc định.
>
> Consent phải tự nguyện, có quyền withdrawal và nêu rõ việc sử dụng external AI provider nếu có. Kết quả cho giảng viên ở cấp cohort và có sample-size warning.
>
> Một vấn đề cần kiểm tra là consent bias: nhóm đồng ý tham gia có thể khác nhóm không tham gia. Vì vậy, phải phân tích selection và missingness trước khi nói về model fairness.

## Slide 19 — Lộ trình nghiên cứu

**Thời lượng:** 45 giây

**Lời thoại**

> Sáu tuần đầu nhằm tạo research-readiness package và reproducible prototype, không phải tạo một paper có kết quả thật bằng mọi giá.
>
> Hai tuần đầu khóa construct, literature, governance và data contract. Tuần ba và bốn xây synthetic replay, baselines và proposed model. Tuần năm dry-run toàn bộ evaluation. Tuần sáu thực hiện adversarial review và quyết định go hoặc iterate cho pilot thật.

## Slide 20 — Rủi ro nghiên cứu

**Thời lượng:** 45–55 giây

**Lời thoại**

> Các rủi ro lớn gồm consent bias, label sparsity, pseudoreplication, productive-struggle false positive, silent-confusion false negative và thiếu external generalization.
>
> Điểm quan trọng là không phải rủi ro nào cũng giải quyết bằng model phức tạp hơn. Một số rủi ro yêu cầu thay đổi sampling, annotation, statistical design hoặc thu hẹp claim.

## Slide 21 — Kết luận và quyết định cần xin ý kiến

**Thời lượng:** 50–60 giây

**Lời thoại**

> Tóm lại, EduPulse nghiên cứu cách biến micro-interactions thành bằng chứng cohort-level có ngữ cảnh và độ bất định. Giá trị của hướng tiếp cận nằm ở việc kết hợp temporal sequence, spatial anchors, cohort convergence, human calibration và privacy-by-design.
>
> Ở giai đoạn này, tôi xin ý kiến về ba quyết định: construct và ranh giới productive struggle đã đủ chặt chưa; hướng novelty có hợp lý so với cộng đồng LA/EDM không; và course, ethics route cùng nguồn label nào phù hợp nhất cho pilot.
>
> Bước tiếp theo là mentor review, literature audit, ethics/data contract, synthetic dry-run và sau đó mới quyết định thu dữ liệu thật.

**Câu kết:**

> Mục tiêu của hệ thống không phải quan sát người học nhiều hơn, mà là biến những tín hiệu tối thiểu, có đồng thuận thành bằng chứng hữu ích và có trách nhiệm hơn cho hoạt động giảng dạy.

## Slide 22–23 — Tài liệu tham khảo

**Thời lượng:** không trình bày, trừ khi được hỏi

**Lời thoại ngắn nếu cần**

> Các nguồn này tạo nền tảng cho bốn nhóm lập luận: confusion và productive struggle, sensor-free affect detection, calibration, và ethics của multimodal learning analytics. Nhóm tài liệu LLM được dùng để định vị cơ hội, hallucination và privacy risk; không được dùng thay bằng chứng thực nghiệm của nghiên cứu này.

---

# Bộ câu hỏi phản biện dự kiến

## “Dwell lâu có nghĩa là sinh viên không hiểu phải không?”

> Không. Dwell là weak contextual signal. Nó chỉ có ý nghĩa khi kết hợp với active dwell, idle detection, chuỗi tương tác, nội dung và sự hội tụ của nhiều người học. Dwell-only cũng là baseline bắt buộc để kiểm tra giá trị bổ sung của phương pháp.

## “Tại sao cần cả `p_individual` và `p_cohort`?”

> `p_individual` mô hình hóa bằng chứng trong một student–page window và giúp liên kết với nhãn ở cấp cá nhân. `p_cohort` tổng hợp evidence của nhiều người học để xác định vùng nội dung đáng được giảng viên xem xét. Đầu ra triển khai ưu tiên `p_cohort`; `p_individual` không được dùng để gắn nhãn hoặc xếp hạng sinh viên.

## “LLM có phải là thành phần novelty chính không?”

> Không tự thân. LLM là một semantic module. Novelty dự kiến nằm ở việc kết hợp temporal–spatial–cohort evidence và human calibration. LLM chỉ được giữ nếu ablation chứng minh incremental value so với các semantic baseline đơn giản hơn.

## “LLM tạo nhãn thì có tiết kiệm chi phí không?”

> LLM có thể gợi ý hoặc ưu tiên mẫu cho người đánh giá, nhưng không được coi output là ground truth. Nếu dùng generated labels để vừa huấn luyện vừa đánh giá, kết luận sẽ bị circular và khó kiểm soát bias.

## “Confusion có thể có lợi, vậy tại sao phải phát hiện?”

> Target không phải mọi confusion mà là unresolved bottleneck. Nghiên cứu có engagement head và outcome linkage để phân biệt productive struggle khỏi khó khăn kéo dài cần hỗ trợ.

## “Tại sao không dùng Transformer?”

> Effective sample size được quyết định bởi participant và course, không phải raw event count. GRU là lựa chọn prototype phù hợp để kiểm tra giá trị của sequence trước. Transformer chỉ nên dùng như challenger khi dữ liệu và baseline cho thấy hợp lý.

## “Nếu mô hình không hơn XGBoost thì nghiên cứu thất bại?”

> Không nhất thiết. Kết quả đó có thể cho thấy sequence model không cần thiết trong bối cảnh này. Contribution khi đó phải được định vị trung thực ở construct, protocol, dataset hoặc empirical finding, không tiếp tục claim model superiority.

## “Hệ thống có cải thiện kết quả học tập không?”

> Paper 1 chưa được phép claim điều đó. Paper 1 đánh giá detection, calibration và educational association. Tác động nhân quả của khuyến nghị cần một intervention hoặc stepped-wedge study ở Paper 2.

## “Dữ liệu hiện có có thể dùng ngay không?”

> Không tự động. Production telemetry chỉ trở thành research data khi có purpose, consent state, provenance, retention, withdrawal và institutional approval phù hợp.

## “Novelty của nghiên cứu là gì trong một câu?”

> Một phương pháp sensor-free kết hợp chuỗi micro-interaction được neo theo vùng nội dung, sự hội tụ cấp cohort và human calibration đa nguồn để phát hiện cognitive bottleneck bằng xác suất được hiệu chuẩn.

---

# Phiên bản rút gọn 3 phút

> Giảng viên thường phát hiện sinh viên gặp khó quá muộn, trong khi những proxy đơn giản như dwell time dễ nhầm đọc kỹ với confusion. EduPulse nghiên cứu liệu chuỗi micro-interaction — gồm scroll reversal, selection, annotation, note và Ask AI — khi được gắn với vị trí trên tài liệu và tổng hợp giữa nhiều sinh viên, có giúp phát hiện unresolved cognitive bottleneck đáng tin cậy hơn hay không.
>
> Bài toán có hai cấp. `p_individual` mô hình hóa bằng chứng trong một student–page window; `p_cohort` tổng hợp nhiều người học để xác định page hoặc region cần giảng viên xem xét. Đầu ra chính là cohort-level, không phải phán xét cá nhân.
>
> Mô hình đề xuất kết hợp GRU sequence encoder, spatial encoder, DeepSets cohort aggregation và multi-task heads cho self-report, teacher label, quiz, exam và engagement. LLM chỉ đóng vai trò semantic copilot để hiểu nội dung và ý định; không tự tạo ground truth. Giá trị LLM được kiểm tra bằng ablation và so sánh với các baseline đơn giản.
>
> Novelty dự kiến nằm ở tổ hợp temporal–spatial evidence, cohort convergence, human calibration và privacy-by-design. Tất cả claim đều phụ thuộc vào preregistered baselines, calibration, course holdout, confidence interval và approved prospective data. Paper 1 không claim hệ thống cải thiện kết quả học tập; câu hỏi đó dành cho intervention study tiếp theo.

