# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** 2A202600440
**Name:** Vũ Hoàng Minh
**Date:** April 15, 2026

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` với 2 bộ dữ liệu và ghi lại kết quả:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | "Agent: Based on my data, the best choice is Laptop at $1200." | 9/10 | Correct identification of electronics, high confidence response |
| Garbage Data (`garbage_data.csv`) | "Agent: I'm not sure how to answer that with the current data." | 3/10 | Fallback response, missing valid electronics in corrupted data |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Khi sử dụng Garbage Data, Agent ghi nhận hàng loạt vấn đề:

**1. Duplicate IDs:** Nhiều record có cùng ID, khiến DataFrame có các hàng bị trùng lặp hoặc bị ghi đè. Trong trường hợp này, Agent không thể tìm được record đúng vì dữ liệu có xung đột.

**2. Wrong Data Types:** Giá tiền được lưu dưới dạng chuỗi (string) thay vì số (float/int). Khi áp dụng `.idxmax()`, Python không thể so sánh chuỗi một cách đúng đắn, dẫn đến kết quả sai hoặc exception.

**3. Outliers:** Những giá trị ngoại lệ như giá âm (price: -10 USD) không được lọc ra đúng cách trước khi đưa vào Agent Simulator. Result: Agent có thể trả về sản phẩm có giá âm.

**4. Null/Empty Values:** Category bị trống hoặc null khiến Agent không thể tìm được electronics category để trả lời: "I'm not sure how to answer that with the current data."

**5. Inconsistent Category Format:** "Electronics", "ELECTRONICS", "electronics" được lưu khác nhau. Khi so sánh với `'electronics'` trong query, sau một hoặc nhiều record gặp chiều và cho kết quả sai.

**Kết quả:** Agent trả lời không có dữ liệu hoặc trả lời sai sau khi xung đột dữ liệu ảnh hưởng tới chất lượng câu trả lời.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** Đồng ý 100%.

Dù có viết prompt chuẩn và chi tiết, nếu dữ liệu brute và không hợp lệ thì Agent vẫn sẽ phân tích không đúng. Trong thực tế:

- **Clean Data:** Agent có khả năng nhận thức tạo ra câu trả lời chính xác, tìm được Laptop ($1200) là sản phẩm điện tử tốt nhất.
- **Garbage Data:** Agent bị buộc phải trả lời "I don't know" vì không tìm thấy các sản phẩm điện tử hợp lệ trong dataset.

**Nhận xét:** Data quality là nền tảng của các hệ thống AI/ML. Không có prompt nào có thể chinh phục dữ liệu lỗi thời. Quy trình ETL + Data Validation là bước đầu tiên rất cần thiết trước khi trải vào AI Agent.

**Điều này chứng minh:** "Garbage in, Garbage out" - từ dữ liệu xấu ra kết quả xấu.
