# Ngày 1 - Bài Tập & Phản Ánh
## Nền Tảng LLM API | Phiếu Thực Hành

**Thời lượng:** 1:30 giờ  
**Cấu trúc:** Lập trình cốt lõi (60 phút) -> Bài tập mở rộng (30 phút)

---

## Phần 1 - Lập Trình Cốt Lõi (0:00-1:00)

Chạy các ví dụ trong Google Colab tại: https://colab.research.google.com/drive/172zCiXpLr1FEXMRCAbmZoqTrKiSkUERm?usp=sharing

Triển khai tất cả TODO trong `template.py`. Chạy `pytest tests/` để kiểm tra tiến độ.

**Điểm kiểm tra:** Sau khi hoàn thành 4 nhiệm vụ, chạy:
```bash
python template.py
```
Bạn sẽ thấy output so sánh phản hồi của GPT-4o và GPT-4o-mini.

---

## Phần 2 - Bài Tập Mở Rộng (1:00-1:30)

### Bài tập 2.1 - Độ Nhạy Của Temperature

Gọi `call_openai` với các giá trị temperature 0.0, 0.5, 1.0 và 1.5 sử dụng prompt **"Hãy kể cho tôi một sự thật thú vị về Việt Nam."**

**Bạn nhận thấy quy luật gì qua bốn phản hồi?** (2-3 câu)
> Khi temperature thấp, đặc biệt là 0.0, câu trả lời thường ổn định, an toàn và ít thay đổi giữa các lần chạy. Khi temperature tăng lên 1.0 hoặc 1.5, phản hồi có xu hướng đa dạng, sáng tạo và bất ngờ hơn, nhưng cũng dễ lan man hoặc kém nhất quán hơn. Vì vậy temperature thể hiện mức độ đánh đổi giữa tính ổn định và tính sáng tạo của mô hình.

**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
> Em sẽ đặt temperature khoảng 0.2 đến 0.5 cho chatbot hỗ trợ khách hàng. Lý do là chatbot hỗ trợ khách hàng cần trả lời chính xác, nhất quán và dễ kiểm soát hơn là quá sáng tạo; mức temperature này vẫn đủ tự nhiên nhưng giảm nguy cơ trả lời sai hoặc lan man.

---

### Bài tập 2.2 - Đánh Đổi Chi Phí

Xem xét kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người dùng thực hiện 3 lần gọi API, mỗi lần trung bình ~350 token.

**Ước tính xem GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này:**
> Tổng số token mỗi ngày là 10.000 * 3 * 350 = 10.500.000 token. Với GPT-4o, chi phí ước tính là 10.500.000 / 1000 * 0.010 = 105 USD/ngày. Với GPT-4o-mini, chi phí ước tính là 10.500.000 / 1000 * 0.0006 = 6.30 USD/ngày. Vì vậy GPT-4o đắt hơn khoảng 105 / 6.30 = 16.7 lần so với GPT-4o-mini cho workload này.

**Mô tả một trường hợp mà chi phí cao hơn của GPT-4o là xứng đáng, và một trường hợp GPT-4o-mini là lựa chọn tốt hơn:**
> GPT-4o xứng đáng dùng khi tác vụ cần suy luận phức tạp, độ chính xác cao hoặc có ảnh hưởng lớn đến quyết định của người dùng, ví dụ phân tích tài liệu pháp lý, tài chính, y tế hoặc xử lý các yêu cầu khách hàng khó. GPT-4o-mini phù hợp hơn cho các tác vụ đơn giản, lặp lại và có số lượng lớn như chatbot FAQ, tóm tắt ngắn, phân loại nội dung hoặc trả lời các câu hỏi phổ biến.

---

### Bài tập 2.3 - Trải Nghiệm Người Dùng với Streaming

**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì non-streaming lại phù hợp hơn?** (1 đoạn văn)
> Streaming quan trọng nhất trong các ứng dụng hội thoại trực tiếp, chatbot, trợ lý viết nội dung hoặc những tác vụ có phản hồi dài, vì người dùng có thể thấy câu trả lời xuất hiện dần thay vì phải chờ toàn bộ kết quả. Điều này giúp trải nghiệm có cảm giác nhanh hơn và tự nhiên hơn, nhất là khi mô hình cần vài giây để sinh phản hồi. Ngược lại, non-streaming phù hợp hơn khi phản hồi ngắn, khi hệ thống cần xử lý toàn bộ kết quả trước khi hiển thị, hoặc khi API được dùng trong backend pipeline cần dữ liệu hoàn chỉnh để kiểm tra, lưu trữ hoặc truyền sang bước tiếp theo.


## Danh Sách Kiểm Tra Nộp Bài

- [x] Tất cả tests pass: `pytest tests/ -v`
- [x] `call_openai` đã triển khai và kiểm thử
- [x] `call_openai_mini` đã triển khai và kiểm thử
- [x] `compare_models` đã triển khai và kiểm thử
- [x] `streaming_chatbot` đã triển khai và kiểm thử
- [x] `retry_with_backoff` đã triển khai và kiểm thử
- [x] `batch_compare` đã triển khai và kiểm thử
- [x] `format_comparison_table` đã triển khai và kiểm thử
- [x] `exercises.md` đã điền đầy đủ
- [x] Sao chép bài làm vào folder `solution` và đặt tên theo quy định
