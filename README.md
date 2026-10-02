# โครงงานปลายภาค: CASMI26 PubChem Popularity Prior

## ข้อมูลผู้จัดทำ

- **ชื่อ:** นายธีรภัทร พิกุลศรี
- **รหัสนักศึกษา:** 68114540308
- **จำนวนสมาชิก:** 1 คน

## รายละเอียดโครงงาน

โครงงานนี้วิเคราะห์ชุดข้อมูล **CASMI26 PubChem Popularity Prior** จาก Kaggle
โดยศึกษาความสัมพันธ์ระหว่างข้อมูลการอ้างอิงสารเคมีกับคะแนนความนิยม
และสร้างแบบจำลอง Regression เพื่อทำนายคะแนนดังกล่าว

Notebook ครอบคลุมเนื้อหาตามโครงสร้างโครงงาน 6 ส่วน:

1. **ภาพรวมข้อมูลและ EDA** — ตรวจสอบข้อมูล ค่าที่หายไป สถิติเชิงพรรณนา และความสัมพันธ์ของตัวแปร
2. **CLO1: พีชคณิตเชิงเส้น** — Covariance matrix, Eigendecomposition และ PCA
3. **CLO2: การเรียนรู้เชิงสถิติ** — Correlation และ Bias-Variance Trade-off
4. **CLO3: การสร้างแบบจำลอง** — เปรียบเทียบ Simple Linear Regression และ Ridge Regression
5. **CLO4: การเลือกโมเดล** — ใช้ 5-Fold Cross-Validation
6. **สรุปผลและเรื่องราวจากข้อมูล**

## ไฟล์สำหรับส่งงาน

- [FINAL_CASMI26_TH.ipynb](./FINAL_CASMI26_TH.ipynb) — Notebook ฉบับสมบูรณ์ภาษาไทย

ไฟล์ `lab15_project_template.ipynb` และไฟล์ที่มีนามสกุล `.ipynb.ipynb` เป็นไฟล์เก่า/ไฟล์สำรอง
ไม่ต้องใช้เป็นไฟล์หลักในการส่งงาน ให้ใช้ `FINAL_CASMI26_TH.ipynb` เท่านั้น

## ชุดข้อมูลและการเตรียมข้อมูล

ดาวน์โหลดชุดข้อมูลโดยใช้ KaggleHub:

```python
import kagglehub

path = kagglehub.dataset_download(
    "dmitriigluzdov/casmi26-pubchem-popularity-prior"
)
print(path)
```

Notebook ใช้ข้อมูลกลุ่ม `pool_*` และสุ่มตัวอย่าง 100,000 แถวด้วย `random_state=42`
เพื่อให้สามารถรันได้บนคอมพิวเตอร์ทั่วไป โดยสร้างตัวแปรสำคัญดังนี้:

- `log_sid`
- `log_pmid`
- `has_pubchem`
- `is_natural_product`
- `target_popularity`

## วิธีรัน Notebook

1. เปิดไฟล์ `FINAL_CASMI26_TH.ipynb` ใน VS Code หรือ Jupyter Notebook
2. ติดตั้งแพ็กเกจที่จำเป็น:

   ```bash
   pip install numpy pandas matplotlib scikit-learn kagglehub
   ```

3. ตรวจสอบว่าเข้าสู่ระบบหรือมีสิทธิ์ดาวน์โหลด dataset จาก Kaggle
4. เลือก Python Kernel
5. กด **Run All**

ผลลัพธ์ที่คาดว่าจะได้ ได้แก่ ตารางสถิติ, กราฟ PCA, กราฟ Bias-Variance,
ผลการประเมินโมเดล และตารางเปรียบเทียบ Cross-Validation

## ผลสรุปโดยย่อ

จากการทดลอง Ridge Regression ให้ผลดีกว่า Simple Linear Regression
เมื่อพิจารณาจากค่า MSE และ R² และ Cross-Validation ใช้ยืนยันว่า Ridge
มีความสามารถในการทำนายกับข้อมูลที่ไม่เคยเห็นได้ดีกว่าโมเดลพื้นฐาน

## หมายเหตุ

คะแนน `target_popularity` เป็นคะแนนที่สร้างจาก log-count ของข้อมูลการอ้างอิง
จึงควรตีความเป็น **prior ของความนิยม** ไม่ใช่การวัดคุณภาพของสารเคมีโดยตรง
