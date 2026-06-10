# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** 26ai.khanhnt2
**Name:** Nguyễn Trọng Khánh
**Date:** 10/06/2026

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Based on my data, the best choice is Laptop at $1200. | 9 | Tra loi dung. Laptop ($1200) la san pham electronics gia tri cao va hop le nhat sau khi da loc bo du lieu rac. |
| Garbage Data (`garbage_data.csv`) | Based on my data, the best choice is Nuclear Reactor at $999999. | 1 | Tra loi sai. Agent bi danh lua boi outlier "Nuclear Reactor" gia $999999 - mot ban ghi vo nghia khong duoc kiem dinh. |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Agent tra loi sai vi no hoat dong theo nguyen tac "Garbage In, Garbage Out": chat luong dau ra phu thuoc hoan toan vao chat luong du lieu dau vao, chu khong phai vao do thong minh cua thuat toan. File `garbage_data.csv` chua nhieu loi chat luong du lieu nghiem trong ma Agent khong he kiem tra. Thu nhat la **outlier (gia tri ngoai lai cuc doan)**: ban ghi "Nuclear Reactor" co gia $999999 hoan toan phi ly, nhung vi Agent dung logic `idxmax()` de chon san pham gia cao nhat, no lap tuc bi danh lua va chon ngay ban ghi rac nay. Thu hai la **duplicate ID** (hai ban ghi cung id = 1 la Laptop va Banana) lam pha vo tinh toan ven cua khoa chinh va co the gay nham lan khi truy van. Thu ba la **sai kieu du lieu (wrong data type)**: cot price chua chuoi "ten dollars" thay vi so, du o tinh huong nay khong bi chon nhung no co the lam crash cac phep tinh so hoc. Thu tu la **null values**: ban ghi "Ghost Item" co id va category deu rong, lam giam do tin cay cua toan bo tap du lieu. Khac voi pipeline da xu ly o `solution.py` (noi ham `validate()` da loai bo gia <= 0 va category rong truoc khi nap), Agent doc thang du lieu rac ma khong co tang kiem dinh nao, nen tat ca cac loi tren deu di thang vao ket qua cuoi cung.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** Dong y.

Thi nghiem chung minh rang du Agent co thuat toan giong het nhau trong ca hai truong hop, ket qua lai khac biet hoan toan chi vi su khac nhau o chat luong du lieu. Mot prompt hay hay mot mo hinh manh cung khong the cuu vang neu du lieu dau vao bi "nhiem doc". Vi vay, dau tu vao **Data Observability** - giam sat va kiem dinh chat luong du lieu (loc outlier, kiem tra kieu, loai null, xu ly duplicate) ngay tu tang pipeline - quan trong hon viec tinh chinh prompt. Du lieu sach la nen mong bat buoc de mot AI Agent dua ra quyet dinh dang tin cay.
