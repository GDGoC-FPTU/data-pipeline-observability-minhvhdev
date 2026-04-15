[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23572344&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** minhvh.dev@gmail.com
**Name:** Vũ Hoàng Minh
**Student ID:** 2A202600440

---

## Mo ta

Bài lab này thực hiện xây dựng một ETL Pipeline tự động để xử lý và làm sạch dữ liệu từ file JSON. Pipeline bao gồm 4 bước chính:
1. Extract: Đọc dữ liệu từ file JSON (raw_data.json)
2. Validate: Kiểm tra và loại bỏ dữ liệu không hợp lệ (giá <= 0, category rỗng)
3. Transform: Chuẩn hóa dữ liệu (title case cho category, tính giá giảm 10%, thêm timestamp)
4. Load: Lưu dữ liệu đã xử lý ra file CSV

Bài lab cũng bao gồm stress test để so sánh hiệu suất pipeline trên dữ liệu sạch vs dữ liệu rác.

---

## Cach chay (How to Run)

### Prerequisites
```bash
pip install pandas
```

### Chay ETL Pipeline
```bash
python solution.py
```

### Chay Agent Simulation (Stress Test)
```bash
python agent_simulation.py
```

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output cua pipeline
├── experiment_report.md     # Bao cao thi nghiem
├── agent_simulation.py      # Stress test script
├── raw_data.json            # Input data
└── README.md                # File nay
```

---

## Ket qua

- **Total records extracted:** 5
- **Valid records:** 3 (price > 0 và category không rỗng)
- **Invalid records dropped:** 2 (1 record có giá âm, 1 record có category rỗng)
- **Output:** 3 records đã được xử lý và lưu trong processed_data.csv
- **Features added:** 
  - discounted_price (giảm 10%)
  - category (chuyển thành Title Case)
  - processed_at (timestamp xử lý)
