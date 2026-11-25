# CNTT1_KyNangPromtingVoiAI_Session09_01

## PROMPT V1 → V2

### 1. Mục đích cải tiến

So sánh Prompt phiên bản V1 và V2 nhằm cải thiện khả năng hiểu yêu cầu, tăng độ chính xác của câu trả lời và hạn chế tình trạng AI tự tạo thông tin không có căn cứ.

### 2. Bảng so sánh V1 và V2

| Tiêu chí | Prompt V1 | Prompt V2 |
| --- | --- | --- |
| Yêu cầu | Chung chung | Cụ thể, rõ ràng |
| Variables | Chưa đầy đủ | Có biến tái sử dụng |
| Output Format | Chưa quy định | Có cấu trúc rõ ràng |
| Hallucination | Chưa kiểm soát | Có quy tắc hạn chế |
| Prompt Injection | Chưa xử lý | Có quy tắc phòng chống |
| Tính tái sử dụng | Thấp | Cao |

### 3. Cải tiến Prompt P01 – Concept Explainer

**Prompt V1:**

```text
Hãy giải thích khái niệm biến trong C.
```

**Nhược điểm:**
- Yêu cầu còn chung chung.
- Chưa xác định trình độ người học.
- Chưa yêu cầu ví dụ minh họa.
- Chưa có định dạng đầu ra.

**Prompt V2:**

```text
Bạn là giảng viên lập trình C.

Hãy giải thích khái niệm {{CONCEPT}}
cho sinh viên có trình độ {{LEVEL}}.

Yêu cầu:
- Sử dụng ngôn ngữ đơn giản, dễ hiểu.
- Giải thích khái niệm rõ ràng.
- Đưa ra ví dụ thực tế.
- Giải thích từng dòng code nếu có.
- Không tự bịa thông tin.

Output Format:
1. Khái niệm.
2. Giải thích.
3. Ví dụ minh họa.
4. Kết luận.
```

**Kết quả cải tiến:** Prompt V2 giúp AI giải thích rõ ràng hơn, phù hợp với trình độ người học và có cấu trúc thống nhất.

### 4. Cải tiến Prompt P02 – Material Summarizer

**Prompt V1:**

```text
Hãy tóm tắt tài liệu sau:
{{MATERIAL}}
```

**Nhược điểm:**
- Có thể bỏ sót nội dung quan trọng.
- Chưa quy định độ dài.
- Chưa kiểm soát việc AI tự bổ sung thông tin.

**Prompt V2:**

```text
Bạn là trợ lý học tập chuyên tóm tắt tài liệu.

Hãy tóm tắt nội dung:
{{MATERIAL}}

Độ dài: {{LENGTH}}.

Yêu cầu:
- Giữ lại các ý chính quan trọng.
- Không làm thay đổi ý nghĩa tài liệu.
- Không tự thêm thông tin ngoài tài liệu.
- Nếu thiếu dữ liệu, hãy thông báo.

Output Format:
1. Chủ đề.
2. Nội dung chính.
3. Các ý quan trọng.
4. Thuật ngữ cần nhớ.
5. Kết luận.
```

**Kết quả cải tiến:** Prompt V2 giúp bản tóm tắt có hệ thống, hạn chế sai lệch thông tin và dễ ghi nhớ hơn.

### 5. Áp dụng Few-shot Prompting cho P04 – Answer Evaluator

**Mục đích:** Cung cấp ví dụ mẫu để AI hiểu cách chấm điểm và nhận xét câu trả lời của sinh viên.

**Prompt Few-shot:**

```text
Bạn là giảng viên đánh giá kiến thức lập trình C.

Ví dụ 1:

Câu hỏi:
Kiểu dữ liệu int trong C dùng để làm gì?

Câu trả lời:
Dùng để lưu số nguyên.

Đáp án:
Dùng để lưu số nguyên.

Kết quả:
Điểm: 10/10.
Nhận xét: Câu trả lời chính xác.

Ví dụ 2:

Câu hỏi:
Kiểu dữ liệu float dùng để làm gì?

Câu trả lời:
Dùng để lưu ký tự.

Đáp án:
Dùng để lưu số thực.

Kết quả:
Điểm: 0/10.
Nhận xét: Câu trả lời chưa chính xác.

NHIỆM VỤ:

Hãy đánh giá câu trả lời sau:

Câu hỏi: {{QUESTION}}
Câu trả lời: {{STUDENT_ANSWER}}
Đáp án: {{REFERENCE}}

Yêu cầu:
- Chấm điểm theo thang 10.
- Nhận xét mức độ chính xác.
- Chỉ ra lỗi sai.
- Đề xuất cách cải thiện.
- Nếu câu trả lời đúng một phần,
  hãy chấm điểm tương ứng.

Output Format:
- Điểm số:
- Nhận xét:
- Điểm đúng:
- Điểm chưa đúng:
- Hướng cải thiện:
```

**Lợi ích của Few-shot:**
- Giúp AI hiểu cách chấm điểm thông qua ví dụ.
- Tạo ra kết quả đánh giá thống nhất.
- Hạn chế nhận xét thiếu rõ ràng.
- Có thể tái sử dụng cho nhiều câu hỏi khác nhau.

---

## DEMO KẾT QUẢ CUỐI

### 1. Dữ liệu đầu vào

**Môn học:** Lập trình C.

**Nội dung tài liệu:**

```c
Vòng lặp for trong C được sử dụng để
thực hiện một đoạn chương trình nhiều lần.

Cấu trúc:

for (khởi_tạo; điều_kiện; cập_nhật) {
    // Câu lệnh
}

Vòng lặp kết thúc khi điều kiện sai.
```

### 2. Demo bước 1 – Material Summarizer (P02)

**Input:**

```text
MATERIAL: Nội dung vòng lặp for trong C.
LENGTH: 100 từ.
FOCUS: Khái niệm và cấu trúc.
```

**Output:**

```text
CHỦ ĐỀ: Vòng lặp for trong C.

NỘI DUNG CHÍNH:
- Vòng lặp for dùng để thực hiện
  một đoạn chương trình nhiều lần.

CẤU TRÚC:
for (khởi_tạo; điều_kiện; cập_nhật) {
    // Câu lệnh
}

CÁC THÀNH PHẦN:
1. Khởi tạo.
2. Điều kiện.
3. Cập nhật.

KẾT LUẬN:
Vòng lặp for kết thúc khi điều kiện sai.
```

### 3. Demo bước 2 – Quiz Generator (P03)

**Input:**

```text
CONTENT: Bản tóm tắt vòng lặp for từ P02.
NUM_QUESTIONS: 3.
DIFFICULTY: Dễ.
QUESTION_TYPE: Trắc nghiệm.
```

**Output:**

**Câu 1:** Vòng lặp for trong C dùng để làm gì?

- A. Khai báo biến.
- B. Lặp lại một đoạn chương trình.
- C. Nhập dữ liệu.
- D. Xuất dữ liệu.

**Đáp án:** B.

**Câu 2:** Vòng lặp for có bao nhiêu thành phần chính trong phần điều khiển?

- A. 1.
- B. 2.
- C. 3.
- D. 4.

**Đáp án:** C.

**Câu 3:** Khi nào vòng lặp for kết thúc?

- A. Khi điều kiện sai.
- B. Khi điều kiện đúng.
- C. Khi chương trình bắt đầu.
- D. Khi khai báo biến.

**Đáp án:** A.

### 4. Demo bước 3 – Answer Evaluator (P04)

**Input – Câu trả lời của sinh viên:**

```text
Câu 1: B.
Câu 2: C.
Câu 3: B.
```

**Output:**

| Câu hỏi | Đáp án đúng | Sinh viên chọn | Kết quả |
| --- | --- | --- | --- |
| Câu 1 | B | B | Đúng |
| Câu 2 | C | C | Đúng |
| Câu 3 | A | B | Sai |

**Điểm số:** 6,67/10.

**Nhận xét:**
- Sinh viên trả lời đúng 2/3 câu hỏi.
- Đã hiểu công dụng của vòng lặp for.
- Đã nắm được cấu trúc vòng lặp.
- Chưa hiểu rõ điều kiện kết thúc vòng lặp.

**Hướng cải thiện:** Ôn tập cách hoạt động của điều kiện trong vòng lặp for.

### 5. Demo bước 4 – Learning Recommendation (P05)

**Input:**

```text
SUBJECT: Lập trình C.
RESULT: 6,67/10.
WEAKNESS: Điều kiện kết thúc vòng lặp.
TIME: 3 ngày.
```

**Output:**

**1. Đánh giá hiện tại:**

Sinh viên đã nắm được kiến thức cơ bản về vòng lặp for nhưng chưa hiểu rõ điều kiện kết thúc.

**2. Kiến thức cần cải thiện:**
- Cách kiểm tra điều kiện trong vòng lặp.
- Khi nào vòng lặp tiếp tục thực hiện.
- Khi nào vòng lặp dừng lại.

**3. Kế hoạch ôn tập:**

| Ngày | Nội dung | Bài tập |
| --- | --- | --- |
| Ngày 1 | Ôn cấu trúc for | Viết vòng lặp từ 1 đến 10 |
| Ngày 2 | Ôn điều kiện | Viết chương trình đếm số |
| Ngày 3 | Tổng hợp kiến thức | Làm 5 câu trắc nghiệm |

**4. Mục tiêu:**
- Hiểu cách hoạt động của vòng lặp for.
- Biết xác định điều kiện dừng.
- Có thể tự viết chương trình sử dụng vòng lặp for.

### 6. Kết quả tổng hợp Demo

| Bước | Chức năng | Kết quả |
| --- | --- | --- |
| 1 | Summarizer | Tạo bản tóm tắt |
| 2 | Quiz Generator | Tạo 3 câu hỏi |
| 3 | Answer Evaluator | Chấm 6,67/10 |
| 4 | Learning Recommendation | Đề xuất kế hoạch 3 ngày |

### 7. Kết luận

Thông qua Demo, hệ thống AI Student Support Assistant đã thực hiện được quy trình hỗ trợ học tập từ tài liệu ban đầu đến đánh giá kết quả và đề xuất nội dung ôn tập.

Các Prompt được liên kết với nhau thông qua Prompt Chaining, giúp tự động hóa quá trình học tập và hỗ trợ sinh viên xác định những kiến thức còn yếu để cải thiện kết quả học tập.
