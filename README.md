[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=24112787&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** 26ai.khanhnt2@vinuni.edu.vn
**Name:** Nguyễn Trọng Khánh
---

## Mo ta

Bai lab nay xay dung mot **ETL Pipeline** tu dong (Extract - Validate - Transform - Load) bang Python va pandas, ket hop tu duy **Data Observability** de giam sat chat luong du lieu.

Nhung gi da lam:
- **Extract:** Doc du lieu tu `raw_data.json`.
- **Validate:** Loai bo cac ban ghi khong hop le (gia <= 0, thieu category) va in ra so luong kept/dropped.
- **Transform:** Tinh `discounted_price` (giam 10%), chuan hoa `category` ve Title Case, them cot `processed_at` (timestamp).
- **Load:** Luu ket qua sach ra `processed_data.csv`.
- **Stress Test:** So sanh phan ung cua AI Agent tren du lieu Sach vs du lieu Rac (`garbage_data.csv`), ghi lai trong `experiment_report.md`.

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
# Buoc 1: Tao file du lieu rac (garbage_data.csv)
python generate_garbage.py

# Buoc 2: Chay mo phong Agent tren ca 2 bo data (Clean vs Garbage)
python agent_simulation.py
```

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output cua pipeline
├── experiment_report.md     # Bao cao thi nghiem
└── README.md                # File nay
```

---

## Ket qua

**ETL Pipeline:** Xu ly 5 ban ghi dau vao -> giu lai **3** ban ghi hop le, loai bo **2** ban ghi loi (id=3 gia <= 0, id=4 thieu category). File `processed_data.csv` duoc tao thanh cong.

**Stress Test (Clean vs Garbage):**
- Clean Data: Agent tra loi dung -> *"the best choice is Laptop at $1200."*
- Garbage Data: Agent tra loi sai do bi outlier danh lua -> *"the best choice is Nuclear Reactor at $999999."*

=> Ket luan: Chat luong du lieu (Data Quality) quyet dinh chat luong dau ra cua AI Agent. Chi tiet phan tich xem trong `experiment_report.md`.
