# 📐 Principle — หลักการเขียนและจัดการไฟล์ .md

> เอกสารกำหนดหลักการ รูปแบบ และแนวทางการเขียนไฟล์ `.md` ทุกไฟล์ในโปรเจกต์
> เพื่อให้ทุก Session / ทุกคนเขียนในรูปแบบเดียวกัน

---

## 1. 📜 หลักการทั่วไป (General Principles)

### 1.1 ภาษา

- ใช้ **ภาษาไทย** เป็นหลักสำหรับเนื้อหาเอกสาร
- ใช้ **ภาษาอังกฤษ** สำหรับ: ชื่อไฟล์, technical terms, code
- ชื่อ Section ใช้ **ไทย + อังกฤษ** ในวงเล็บ

### 1.2 ชื่อไฟล์

- ใช้ **kebab-case** (ตัวพิมพ์เล็ก + ขีดกลาง)
- นามสกุล `.md` เท่านั้น
- ไฟล์ `.md` ทั้งหมดเก็บใน folder `ai-workflow/`

ตัวอย่าง:
```
❌ ผิด: startUp.md, Start-up.md, Start_up.md, START-UP.MD
✅ ถูก: start-up.md, hand-over.md, structure-file.md
```

### 1.3 Encoding

- ใช้ **UTF-8** เสมอ, Line ending: **LF**

---

## 2. 📝 รูปแบบการเขียน (Writing Format)

### 2.1 โครงสร้างไฟล์ .md ทุกไฟล์

แต่ละไฟล์ .md ต้องมีโครงสร้างดังนี้:

```markdown
# 🎨 ไฟล์ที่ 1 (File Name)

> Blockquote อธิบายว่าไฟล์นี้ทำอะไร
> เขียนสั้นๆ 1-3 บรรทัด

---

## 1️⃣ Section แรก

เนื้อหา...

---

## 2️⃣ Section ที่สอง

เนื้อหา...

---

## 📝 Change Log

| วันที่ | เวอร์ชัน | รายละเอียด |
| ------ | -------- | ---------- |
| YYYY-MM-DD | X.Y | คำอธิบาย |
```

**กฎ:**
- H1 (`#`) มีได้แค่ 1 ต่อไฟล์ + emoji นำหน้า
- Blockquote (`>`) อยู่ใต้ H1 เสมอ
- แบ่ง Section ด้วย `---` (horizontal line)
- Change Log เป็น Section สุดท้ายทุกไฟล์

### 2.2 Status Icons

ใช้ icon เหล่านี้เพื่อแสดงสถานะ:

| Icon | ความหมาย | ใช้กับ |
| ---- | -------- | ----- |
| ⬜ | ยังไม่เริ่ม (Not Started) | Task status, Checklist |
| 🔄 | กำลังทำ (In Progress) | Task status, Phase status |
| ✅ | เสร็จแล้ว (Complete) | Task status, Phase status |
| 🔴 | Priority สูง / Must Have | Feature priority, Issue severity |
| 🟡 | Priority กลาง / Should Have | Feature priority, Issue severity |
| 🟢 | Priority ต่ำ / Nice to Have | Feature priority, Issue severity |
| ⚠️ | Warning / Caution | Important notes |
| 💡 | Idea / Suggestion | Thoughts, Insights |
| 🐛 | Bug | Issue type |
| 🚀 | New feature / Enhancement | Feature type |

### 2.3 Placeholder

ใช้ `<!-- comment -->` สำหรับจุดที่ยังไม่กรอก:

```markdown
<!-- TODO: เพิ่มคำอธิบาย workflow ที่นี่ -->
<!-- หรือ: อธิบายว่า feature นี้ต้อง integration กับ feature อื่น -->
```

---

## 3. 📊 Markdown Components

### 3.1 ตาราง (Tables)

ใช้สำหรับข้อมูลเปรียบเทียบหรือข้อมูลแบบ structured:

```markdown
| คอลัมน์ 1 | คอลัมน์ 2 | คอลัมน์ 3 |
| -------- | -------- | -------- |
| ค่า 1 | ค่า 2 | ค่า 3 |
```

### 3.2 Blockquote

ใช้เน้นข้อความสำคัญ:

```markdown
> **⚡ สำคัญ:** เข้าใจกฎนี้ให้ดี
> เพราะมันส่งผลต่อทั้งโปรเจกต์
```

### 3.3 Checklist

ใช้ติดตาม task:

```markdown
- [x] Task ที่เสร็จแล้ว
- [ ] Task ที่ยังต้องทำ
- [ ] อีกตัว
```

### 3.4 Code Block

ใช้แสดง command, config, code snippet:

```markdown
\`\`\`javascript
// JavaScript code
console.log("Hello");
\`\`\`

\`\`\`bash
# Bash command
npm install
\`\`\`

\`\`\`json
{
  "name": "js_tesseract_opencv"
}
\`\`\`
```

### 3.5 List

**Unordered List:**
```markdown
- Item 1
- Item 2
  - Sub item 2.1
  - Sub item 2.2
```

**Ordered List:**
```markdown
1. First step
2. Second step
   1. Sub step 2.1
   2. Sub step 2.2
```

---

## 4. 📄 แนวทางเฉพาะแต่ละไฟล์

### 4.1 start-up.md

**จุดประสงค์:** Onboarding guide สำหรับคนใหม่หรือ session ใหม่

**โครงสร้าง:**
1. H1 + Blockquote
2. "ลำดับการอ่านเอกสาร" (Reading Order) — ขั้นตอน 1-5
3. "สรุปสั้นๆ" (Quick Summary)

**กฎ:**
- ต้องเรียงลำดับไฟล์จากสำคัญที่สุดไปน้อยที่สุด
- ใช้ "👉" icon เพื่อชี้ไปที่ไฟล์
- อธิบายว่า "ทำไมต้องอ่าน" และ "จะได้รู้อะไร"

---

### 4.2 prd.md (Product Requirements Document)

**จุดประสงค์:** Single source of truth สำหรับ requirement ทั้งหมด

**โครงสร้าง:**
1. H1 + Blockquote
2. Section 1: ภาพรวมโปรเจกต์
   - 1.1 วัตถุประสงค์
   - 1.2 หลักการพัฒนา (Development Principle)
   - 1.3 ปัญหาที่ต้องแก้ไข
   - 1.4 กลุ่มผู้ใช้งาน
3. Section 2: Technology Stack (ตาราง)
4. Section 3: Functional Requirements (Features)
   - Format: ตาราง สำหรับแต่ละ feature
5. Section 4: Pages / Screens
6. Section 5: API Endpoints (ตาราง)
7. Section 6: Database Design
8. Section 7: Non-Functional Requirements

**กฎ:**
- ทุก Feature ต้องมี: Priority, Description, User Story, Acceptance Criteria
- Priority ใช้ Icon: 🔴 Must Have, 🟡 Should Have, 🟢 Nice to Have
- ห้ามมีความขัดแย้ง requirement

---

### 4.3 hand-over.md

**จุดประสงค์:** ส่งต่องาน + สถานะปัจจุบัน

**โครงสร้าง:**
1. H1 + Blockquote
2. สถานะปัจจุบัน (ตาราง 3 row: Phase, Status, Last updated)
3. สิ่งที่เสร็จแล้ว (✅ section + checklist)
4. งานกำลังทำค้าง (🔨 section + ตาราง)
5. สิ่งที่ต้องทำต่อ (📋 section + ordered list)
6. ปัญหา/Blockers (⚠️ section + ตาราง)
7. การตัดสินใจที่รอ (💡 section + ตาราง)
8. ไฟล์ที่เกี่ยวข้อง (📎 section + ตาราง)
9. Notes

**กฎ:**
- ⚡ **ต้องอัปเดตก่อนจบ session เสมอ**
- ใช้ Icon status: ⬜ Not started, 🔄 In progress, ✅ Complete
- ใช้ Icon priority: 🔴 High, 🟡 Medium, 🟢 Low

---

### 4.4 structure-file.md

**จุดประสงค์:** Directory tree + folder description

**โครงสร้าง:**
1. H1 + Blockquote
2. Root Directory (code block + tree format)
3. Directory Size Estimate (ตาราง)
4. Key Relationships (text + diagram)
5. Change Log

**กฎ:**
- Tree format ต้องแม่นยำ
- comment ต่อหลัง folder/file เพื่ออธิบาย
- ใช้ emoji เพื่อจัดหมวดหมู่ (📁 folder, 🔌 API, 🎨 UI)
- ต้อง match กับโครงสร้าง project จริง

---

### 4.5 principle.md

**จุดประสงค์:** Documentation + Coding standards

**โครงสร้าง:**
1. H1 + Blockquote
2. Section 1: หลักการทั่วไป (Language, File naming, Encoding)
3. Section 2: รูปแบบการเขียน (Structure, Icons, Placeholders)
4. Section 3: Markdown Components (Tables, Blockquotes, Checklists, Code blocks, Lists)
5. Section 4: แนวทางเฉพาะแต่ละไฟล์
6. Section 5: Dependency Map (Cross-file impact)
7. Section 6: Re-open Phase rules
8. Section 7: Session workflow guidelines
9. Section 8: Summary table

**กฎ:**
- ไฟล์นี้ใหญ่ที่สุด — ต้องครบถ้วน
- ต้องให้ตัวอย่าง ✅/❌ เพื่อ clarity

---

### 4.6 checklist.md

**จุดประสงค์:** Overall progress tracking ของทั้งโปรเจกต์

**โครงสร้าง:**
1. H1 + Blockquote
2. Checklist ย่อย (แยกตาม stream) — ตาราง link
3. Phase Overview (ตาราง phase x stream)

**กฎ:**
- ต้อง link ไปที่ checklist ของแต่ละ stream
- Status ใช้: ⬜ Not started, 🔄 In progress, ✅ Complete
- ต้อง sync กับ `implement-plan-xx/checklist.md`

---

### 4.7 implement-plan-{stream}/hand-over.md

**จุดประสงค์:** ส่งต่องาน stream-specific

**โครงสร้าง:**
1. H1 + Blockquote
2. สถานะ (ตาราง)
3. เสร็จแล้ว (✅)
4. กำลังทำ (🔨)
5. ต้องทำต่อ (📋)
6. ไฟล์ที่เกี่ยวข้อง (📎)

---

### 4.8 implement-plan-{stream}/checklist.md

**จุดประสงค์:** Stream-specific progress tracking

**โครงสร้าง:**
1. H1 + Blockquote
2. Phase 0, 1, 2, ... (แต่ละ phase เป็น checklist)

**กฎ:**
- Task ต้องแสดง dependency ชัดเจน
- ใช้ nested checklist สำหรับ sub-task

---

### 4.9 implement-plan-{stream}/phase-XX.md

**จุดประสงค์:** Phase plan ของแต่ละ stream

**โครงสร้าง:**
1. H1 + Blockquote
2. 🎯 เป้าหมาย (Goals)
3. 📋 Tasks (Checklist หรือ ตาราง)
4. 📚 Resources / References
5. ⚠️ Risks / Considerations

---

### 4.10 design-{stream}.md

**จุดประสงค์:** Architecture + Design convention

**โครงสร้าง:**
1. H1 + Blockquote
2. Section 1: Architecture Overview
3. Section 2: Project Structure
4. Section 3: Design Convention (Naming, Folder structure, Coding style)
5. Section 4: Key Components / Modules
6. Change Log

**กฎ:**
- ต้องดึง Convention จากโค้ด จริง
- ต้องใช้ Diagram ถ้า complex

---

### 4.11 issue-log.md

**จุดประสงค์:** Bug & issue tracker

**โครงสร้าง:**
1. H1 + Blockquote
2. Active Issues (ตาราง)
3. Resolved Issues (ตาราง)
4. (Optional) Known Issues

**ตาราง columns:**
| ID | Issue | Severity | Status | Date Found | Assigned To |

---

### 4.12 impact-analysis.md

**จุดประสงค์:** Change impact map

**โครงสร้าง:**
1. H1 + Blockquote
2. วิธีใช้งาน (How to use)
3. Impact Map (ตาราง)
   - Column: เมื่อเปลี่ยน... → ไฟล์ที่กระทบ → Severity

**กฎ:**
- ต้องครอบคลุม major changes ทั้งหมด
- Severity: 🔴 High, 🟡 Medium, 🟢 Low

---

## 5. 🗺️ Dependency Map (ผลกระทบข้ามไฟล์)

เมื่อแก้ไขไฟล์ต่อไปนี้ ต้องไปอัปเดตไฟล์อื่นด้วย:

| ถ้าแก้... | ต้องไปแก้ |
| ------- | ------- |
| `prd.md` | `design-xx.md`, `implement-plan-*/`, `hand-over.md`, `checklist.md` |
| `design-xx.md` | `implement-plan-xx/`, `structure-file.md`, `hand-over.md` |
| `structure-file.md` | `design-xx.md`, `implement-plan-*/`, `hand-over.md` |
| `implement-plan-xx/phase-YY.md` | `checklist.md`, `hand-over.md`, parent `implement-plan-xx/hand-over.md` |
| `issue-log.md` | `hand-over.md`, `implement-plan-xx/hand-over.md` |

---

## 6. 🔄 กฎการ Re-open Phase

เมื่อ Change Requirement กระทบ Phase ที่ ✅ เสร็จแล้ว:

1. **สร้าง patch ใหม่:** `phase-XX-patch-N.md` (N = 1, 2, 3...)
2. **ระบุต้นเหตุ:** CR Number หรือ Issue ID ที่เป็นต้น
3. **เปลี่ยนสถานะ Phase:** จาก ✅ เป็น 🔄 ใน `checklist.md`
4. **เมื่อ Patch เสร็จ:** เปลี่ยนกลับเป็น ✅

⛔ **ห้ามแก้ไข `phase-XX.md` ต้นฉบับ** ที่เสร็จแล้ว

---

## 7. ✍️ แนวทาง Session ทำงาน

### 7.1 เริ่ม Session ใหม่

1. อ่าน `ai-workflow/start-up.md`
2. อ่าน `ai-workflow/hand-over.md`
3. อ่าน `ai-workflow/principle.md` (ไฟล์นี้)
4. อ่าน `ai-workflow/checklist.md`
5. เลือก stream + phase ที่จะทำ
6. อ่าน `implement-plan-xx/phase-YY.md`
7. เริ่มทำงาน

### 7.2 จบ Session

1. อัปเดต `implement-plan-xx/checklist.md` → Task status
2. อัปเดต `implement-plan-xx/hand-over.md` → Progress
3. อัปเดต `ai-workflow/checklist.md` → Overall status
4. อัปเดต `ai-workflow/hand-over.md` → Summary
5. **Commit ไป git** ก่อนจบ
6. Push ไป remote (ถ้ามี)

### 7.3 เพิ่มไฟล์ .md ใหม่

1. ตั้งชื่อตาม convention (kebab-case)
2. ใช้โครงสร้างพื้นฐาน (H1 + Emoji + Blockquote)
3. เพิ่ม guideline ใน `principle.md` section 4
4. อัปเดต `structure-file.md`
5. อัปเดต `hand-over.md`
6. Commit + Push

---

## 8. 📎 สรุปไฟล์ .md ในโปรเจกต์

| ไฟล์ | Emoji | จุดประสงค์ | Folder |
| --- | ---- | --------- | ------ |
| start-up.md | 🚀 | Onboarding guide | ai-workflow/ |
| prd.md | 📋 | Product requirements | ai-workflow/ |
| hand-over.md | 🔄 | Session hand-over | ai-workflow/ |
| structure-file.md | 📁 | Directory mapping | ai-workflow/ |
| principle.md | 📐 | Standards & guidelines | ai-workflow/ |
| checklist.md | ✅ | Overall progress | ai-workflow/ |
| design-{stream}.md | 🎨 | Architecture | ai-workflow/ |
| issue-log.md | 🐛 | Bug tracker | ai-workflow/ |
| impact-analysis.md | 🔍 | Change impact | ai-workflow/ |
| implement-plan-{stream}/hand-over.md | 🔄 | Stream hand-over | ai-workflow/implement-plan-xx/ |
| implement-plan-{stream}/checklist.md | ✅ | Stream progress | ai-workflow/implement-plan-xx/ |
| implement-plan-{stream}/phase-XX.md | 📋 | Phase plan | ai-workflow/implement-plan-xx/ |

---

## 📝 Change Log

| วันที่ | เวอร์ชัน | รายละเอียด |
| ------ | -------- | ---------- |
| 2026-03-12 | 1.0 | สร้างหลักการเริ่มต้น (auto-generated จาก init-ai-workflow) |

