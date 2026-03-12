# 🔍 Impact Analysis (แผนที่ผลกระทบ)

> เมื่อ **Requirement เปลี่ยน** → ไฟล์นี้บอกว่าต้องไปแก้ไฟล์ไหนบ้าง
> **⚠️ ทุกครั้งที่มีการเปลี่ยนแปลง Requirement ต้องเปิดไฟล์นี้ก่อนเสมอ**

---

## 📌 วิธีใช้งาน

1. ระบุว่าสิ่งที่เปลี่ยนจัดอยู่ในหมวดไหน
2. ดูรายการไฟล์ที่ต้องแก้ไข
3. ไล่แก้ทีละไฟล์ → ติ๊กเมื่อแก้แล้ว
4. อัปเดต `hand-over.md` เมื่อแก้เสร็จ

---

## 🗺️ Impact Map

| # | เมื่อเปลี่ยน... | ไฟล์ที่กระทบ | Severity |
| --- | ----- | --------- | --------- |
| 1 | **Role / Permission** | prd.md, design-fullstack.md, implement-plan-fullstack/ | 🔴 High |
| 2 | **หน้าจอ UI (เพิ่ม/ลบ)** | prd.md, design-fullstack.md, structure-file.md, implement-plan-fullstack/ | 🔴 High |
| 3 | **API Endpoint** | prd.md, design-fullstack.md, implement-plan-fullstack/, interface-contract.md (if exists) | 🔴 High |
| 4 | **Entity / DB Schema** | prd.md, design-fullstack.md, implement-plan-fullstack/ | 🟡 Medium |
| 5 | **Tech Stack** | prd.md, design-fullstack.md, hand-over.md, implement-plan-fullstack/phase-00.md | 🟡 Medium |
| 6 | **Feature ใหม่ (Core)** | prd.md, design-fullstack.md, implement-plan-fullstack/, checklist.md, structure-file.md | 🔴 High |
| 7 | **Processing Flow** | prd.md, design-fullstack.md, implement-plan-fullstack/ | 🟡 Medium |
| 8 | **Input Validation Rule** | prd.md, design-fullstack.md, implement-plan-fullstack/phase-xx.md | 🟢 Low |
| 9 | **Error Handling Strategy** | design-fullstack.md, implement-plan-fullstack/ | 🟡 Medium |
| 10 | **UI Component** | design-fullstack.md, implement-plan-fullstack/design-fullstack.md | 🟢 Low |
| 11 | **Library/Dependency** | prd.md, design-fullstack.md, structure-file.md, package.json | 🟡 Medium |

---

## 📝 Change Log

| วันที่ | เวอร์ชัน | รายละเอียด |
| ------ | -------- | ---------- |
| 2026-03-12 | 1.0 | สร้าง Impact Analysis (auto-generated จาก init-ai-workflow) |

