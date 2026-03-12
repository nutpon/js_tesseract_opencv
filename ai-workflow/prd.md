# 📋 Product Requirements Document (PRD)

> เอกสารความต้องการของโปรเจกต์ **Insurance OCR POC**
> ⚠️ ไฟล์นี้คือ **Single Source of Truth** ของ Requirement ทั้งหมด

---

## 1. 🎯 ภาพรวมโปรเจกต์ (Project Overview)

### 1.1 วัตถุประสงค์ (Objective)

**Insurance OCR POC** (Proof of Concept) เป็นเว็บแอปพลิเคชันแบบ Single-Page ที่ใช้ **OpenCV.js** และ **Tesseract.js** เพื่อ:

- 📄 สกัดข้อความจากเอกสาร A4 ที่ซับซ้อน (เช่น Insurance Policies)
- 🖼️ ประมวลผลภาพด้วย OpenCV.js เพื่อเพิ่มความคมชัด (enhance text readability)
- 🔤 ทำ OCR โดยรองรับภาษาไทยและอังกฤษพร้อมกัน
- ⚡ ทำให้เร็วที่สุด Proof of Concept (ต้องทำได้ใน Single HTML file)

### 1.2 หลักการพัฒนา (Development Principle)

โปรเจกต์นี้ออกแบบให้เป็น **Single-Page Web Application (SPA)** ที่:

| หัวข้อ | รายละเอียด |
| --- | ---------- |
| **Platform** | Browser-only (สามารถเรียกใช้ผ่าน HTML file ได้โดยตรง) |
| **Architecture** | Single HTML file ที่มี embedded CSS และ JavaScript |
| **Libraries** | CDN-only (ไม่ต้อง npm install) |
| **Technology** | Vanilla HTML5 + CSS3 + JavaScript (ไม่ใช้ React/Vue) |

> 📌 **Portability First** — ตัวแฟ้ม index.html เพียงไฟล์เดียว ดาวน์โหลดแล้วเปิดในเบราว์เซอร์ได้ทันที

### 1.3 ปัญหาที่ต้องการแก้ไข (Problem Statement)

- ต้องการ **Proof of Concept ที่เร็ว** สำหรับการทดสอบ OCR บนเอกสารประกันภัยที่ซับซ้อน
- ต้องการเครื่องมือที่ **ไม่ต้องติดตั้งใดๆ** (เพียงแค่ HTML file + browser)
- ต้องการประมวลผลภาพให้เหมาะสมกับ **เอกสาร A4 ที่มีพื้นหลัง/watermarks**
- ต้องการรองรับ **ภาษาไทยและอังกฤษ** เพื่อให้ OCR มีความแม่นยำสูง

### 1.4 กลุ่มผู้ใช้งาน (Target Users)

| กลุ่มผู้ใช้ | คำอธิบาย | สิทธิ์หลัก |
| ---------- | ------- | --------- |
| **Developer / Tester** | ผู้ทดสอบ OCR capability | Upload image, process, tweak settings, view results |
| **Proof of Concept Validator** | ผู้ประเมินความเป็นไปได้ | See raw text extraction, execution time, quality metrics |

---

## 2. 🛠️ Technology Stack

| Component | Technology | เวอร์ชัน | หมายเหตุ |
| --------- | ---------- | -------- | -------- |
| **Frontend** | Vanilla HTML5 + CSS3 + JavaScript | Latest | No framework (zero setup) |
| **OCR Library** | Tesseract.js | Latest via CDN | WASM-based OCR |
| **CV Library** | OpenCV.js | Latest via CDN | WASM-based image processing |
| **Deployment** | Single HTML File | N/A | Embed all CSS & JS inline |
| **Package Manager** | None (CDN only) | N/A | No npm, no build step |
| **Browser Support** | Modern browsers | Chrome 60+, Firefox 55+, Safari 12+ | Must support WebAssembly |

> ⚡ **Key Constraint:** All code in ONE HTML file (index.html) loaded via CDN scripts

---

## 3. 📦 Functional Requirements

### 3.1 Core Features

#### Feature 1: Image Upload & Preview

| รายละเอียด | ค่า |
| ---------- | --- |
| **Priority** | 🔴 Must Have |
| **คำอธิบาย** | ผู้ใช้สามารถอัปโหลดไฟล์รูปภาพ A4 และเห็นตัวอย่างก่อนประมวลผล |
| **User Story** | ในฐานะผู้ทดสอบ ฉันต้องการอัปโหลดรูปสแกนของเอกสารประกันภัย เพื่อให้มั่นใจว่าไฟล์ถูกต้อง |
| **Acceptance Criteria** | ✓ สามารถอัปโหลดไฟล์ได้ / ✓ แสดงตัวอย่างรูปบน Canvas (Canvas 1) / ✓ รองรับ JPG, PNG, GIF, BMP / ✓ มีการตรวจสอบว่า OpenCV โหลดเสร็จแล้ว |

#### Feature 2: Image Pre-processing (OpenCV.js)

| รายละเอียด | ค่า |
| ---------- | --- |
| **Priority** | 🔴 Must Have |
| **คำอธิบาย** | ใช้ OpenCV.js เพื่อประมวลผลภาพให้คมชัดสำหรับ OCR ที่ดีขึ้น |
| **User Story** | ในฐานะผู้ทดสอบ ฉันต้องการให้ระบบทำการ filter เอกสารเพื่อลดเสียงรบกวนและเพิ่มความชัด |
| **Processing Pipeline** | ✓ Convert Grayscale / ✓ Apply Adaptive Thresholding or Otsu's Thresholding / ✓ Display on Canvas 2 |
| **Additional** | ✓ ผู้ใช้สามารถปรับค่า threshold ได้ (optional tweaking) |

#### Feature 3: OCR Text Extraction (Tesseract.js)

| รายละเอียด | ค่า |
| ---------- | --- |
| **Priority** | 🔴 Must Have |
| **คำอธิบาย** | ใช้ Tesseract.js เพื่อสกัดข้อความจากรูปที่ประมวลผลแล้ว |
| **User Story** | ในฐานะผู้ทดสอบ ฉันต้องการให้ระบบสกัดข้อความจากภาพและแสดงผลลัพธ์ พร้อมเวลาที่ใช้ |
| **Acceptance Criteria** | ✓ รองรับ Thai (tha) + English (eng) / ✓ ใช้ PSM mode 1 หรือ 3 สำหรับเอกสาร / ✓ แสดง Progress indicator ✓ บันทึกเวลา execution |

#### Feature 4: Output Display & Status Tracking

| รายละเอียด | ค่า |
| ---------- | --- |
| **Priority** | 🔴 Must Have |
| **คำอธิบาย** | แสดงข้อความที่สกัดได้และสถานะการประมวลผล |
| **Components** | ✓ Textarea/Div สำหรับแสดง raw text / ✓ Status indicator (Loading, Pre-processing, OCR progress) / ✓ Execution time metric |
| **User Story** | ในฐานะผู้ทดสอบ ฉันต้องการเห็นข้อความที่สกัดได้และความก้าวหน้า เพื่อทำความเข้าใจว่ากำลังประมวลผลอยู่ |

#### Feature 5: Repeat Workflow

| รายละเอียด | ค่า |
| ---------- | --- |
| **Priority** | 🟡 Should Have |
| **คำอธิบาย** | ผู้ใช้สามารถอัปโหลดภาพใหม่และทำให้ผลลัพธ์เคลียร์อัตโนมัติ |
| **User Story** | ในฐานะผู้ทดสอบ ฉันต้องการทำความเสี่ยงหลายไฟล์โดยไม่ต้องโหลดหน้าใหม่ |
| **Acceptance Criteria** | ✓ Canvas และ textarea เคลียร์เมื่ออัปโหลดไฟล์ใหม่ / ✓ สถานะรีเซ็ต |

---

## 4. 📄 UI Layout (Single-Page Application)

### 4.1 Layout Structure

The application is a **Single Page** with 3 sections arranged vertically or side-by-side:

| ส่วน | รายละเอียด |
| ---- | --------- |
| **Input Section** | <input type="file"> + "Start Processing" button |
| **Process Pipeline** | Canvas 1 (Original) + Canvas 2 (Processed) side-by-side |
| **Output Section** | Textarea for raw text + Status indicator + Execution time |

### 4.2 Detailed Layout Components

```
┌─────────────────────────────────────────────────────────────┐
│          Insurance OCR POC - Single Page Layout             │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  📥 INPUT SECTION                                           │
│  ┌──────────────────────────────────────────────────────┐   │
│  │ Choose File: [Upload Button]                         │   │
│  │ [Start Processing Button] [Reset Button]             │   │
│  │ ⚠️ Status: Waiting for input...                     │   │
│  └──────────────────────────────────────────────────────┘   │
│                                                              │
│  🖼️  PROCESS PIPELINE (Side-by-Side)                       │
│  ┌──────────────────────┬──────────────────────┐            │
│  │  Canvas 1:           │  Canvas 2:           │            │
│  │  Original Image      │  Processed Image     │            │
│  │                      │  (Grayscale +        │            │
│  │  [Image Renders]     │   Thresholding)      │            │
│  │                      │  [Image Renders]     │            │
│  └──────────────────────┴──────────────────────┘            │
│                                                              │
│  📄 OUTPUT SECTION                                          │
│  ┌──────────────────────────────────────────────────────┐   │
│  │ Extracted Text (Raw):                                │   │
│  │ ┌──────────────────────────────────────────────────┐ │   │
│  │ │ [Textarea with extracted text will appear here] │ │   │
│  │ │                                                  │ │   │
│  │ │                                                  │ │   │
│  │ └──────────────────────────────────────────────────┘ │   │
│  │                                                      │   │
│  │ ⏱️ Execution Time: 0.00s                             │   │
│  │ 🔄 Status: Loading OpenCV... → Pre-processing... → │   │
│  │    Running OCR... 45%                              │   │
│  └──────────────────────────────────────────────────────┘   │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

### 4.3 UI Elements Details

| Element | Type | Purpose |
| ------- | ---- | ------- |
| File Input | `<input type="file" accept="image/*">` | Upload A4 document |
| Start Button | `<button>` | Trigger processing pipeline |
| Reset Button | `<button>` | Clear all and reset |
| Canvas 1 | `<canvas id="originalCanvas">` | Display original image |
| Canvas 2 | `<canvas id="processedCanvas">` | Display OpenCV processed image |
| Output Textarea | `<textarea readonly>` | Display raw extracted text |
| Status Indicator | `<div id="status">` | Show "Loading...", "Pre-processing...", "OCR...X%" |
| Execution Time | `<span id="execTime">` | Display total time in seconds |

---

## 5. 🔌 Processing Pipeline (Client-Side Only)

Since this is a Single-Page Application with no backend, all processing happens in the browser.

### 5.1 Processing Flow

| Step | Component | Input | Output | Details |
| ---- | --------- | ----- | ------ | ------- |
| 1 | File Upload | Image File | Image Object | User selects file from disk |
| 2 | Canvas Render (Original) | Image Object | Canvas 1 | Display original on canvas |
| 3 | OpenCV Processing | Canvas 1 | cv.Mat | Convert to grayscale, apply thresholding |
| 4 | Canvas Render (Processed) | cv.Mat | Canvas 2 | Display processed image |
| 5 | Tesseract OCR | Canvas 2 | Raw Text | Run OCR with tha+eng languages |
| 6 | Output Display | Raw Text | Textarea | Show extracted text to user |
| 7 | Timing Calculation | Start → End | Execution Time | Display total processing time |

### 5.2 OpenCV.js Processing Steps (Sequential)

```javascript
// Step 2.1: Load image to Canvas 1
// Step 2.2: Convert to grayscale (cv.cvtColor with cv.COLOR_RGBA2GRAY)
// Step 2.3: Apply adaptive thresholding OR Otsu's thresholding
//   - Option A: cv.adaptiveThreshold (for better results)
//   - Option B: cv.threshold with cv.THRESH_OTSU
// Step 2.4: Render processed cv.Mat to Canvas 2
```

### 5.3 Tesseract.js Processing Configuration

```javascript
Tesseract.recognize(canvasImage, 'tha+eng', {
  logger: m => console.log(m),  // Log progress
  // PSM options:
  // 0: Orientation and script detection (OSD) only
  // 1: Automatic page segmentation with OSD
  // 3: Fully automatic page segmentation
  psm: 1 // or 3 for multi-column documents
})
```

---

## 6. 🗄️ Storage (Not Required)

This is a Proof of Concept with **NO persistence**:
- No database needed
- No file storage needed
- All processing happens in-memory
- Results are only displayed on screen

> 📌 If future version needs persistence, can add localStorage or IndexedDB

---

## 7. ⚙️ Non-Functional Requirements

| หมวด | Requirement |
| ---- | ----------- |
| **Performance** | Response time < 10 seconds for A4 image processing + OCR |
| **Browser Support** | Chrome 60+, Firefox 55+, Safari 12+, Edge 79+ (must support WebAssembly) |
| **Portability** | Single index.html file, can be run locally without server |
| **Accessibility** | Basic accessibility (proper labels, status messages) |
| **File Size** | Keep HTML file < 5MB (including embedded CSS) |
| **Code Quality** | Heavily commented, modular structure for easy tweaking |
| **Error Handling** | Graceful errors if OpenCV fails to load, informative user messages |
| **Responsiveness** | Support desktop resolutions, works on different screen sizes |

---

## 8. 🔐 Constraints & Assumptions

### 8.1 Hard Constraints

- ✅ **Single HTML File** — All code embedded in one index.html
- ✅ **No Build Step** — No npm install, no webpack, no build process
- ✅ **CDN Libraries Only** — Tesseract.js and OpenCV.js via CDN
- ✅ **Vanilla JavaScript** — No React, Vue, or other frameworks
- ✅ **Client-Side Only** — No backend server needed
- ✅ **Check OpenCV Load** — Must verify cv object is loaded before allowing upload

### 8.2 Design Constraints

- ✅ **Heavy Comments** — Code must be heavily commented for easy tweaking
- ✅ **Modular Functions** — Separate functions for OpenCV processing, Tesseract OCR, UI updates
- ✅ **Easy Threshold Tuning** — Developers can easily adjust OpenCV threshold values
- ✅ **Easy PSM Mode Change** — Developers can easily switch Tesseract PSM modes

### 8.3 Assumptions

- Modern browsers with WebAssembly support will be used
- Users will have a stable internet connection (to load WASM modules from CDN)
- A4 document images will be clear and readable
- Input images will be in common formats (JPG, PNG)

---

## 9. 📋 Glossary & Abbreviations

| Term | Definition |
| ---- | ---------- |
| **OCR** | Optical Character Recognition — extracting text from images |
| **A4** | Standard paper size used for documents |
| **OpenCV.js** | JavaScript binding for OpenCV (image processing library) |
| **Tesseract.js** | JavaScript OCR engine |
| **PSM** | Page Segmentation Mode (Tesseract parameter) |
| **WASM** | WebAssembly — binary format for browser execution |
| **Canvas** | HTML5 canvas element for rendering images |
| **Thresholding** | Converting grayscale image to binary (black & white) |
| **Grayscale** | Single-channel image (no color, only brightness) |
| **POC** | Proof of Concept |
| **SPA** | Single-Page Application |
| **CDN** | Content Delivery Network |

---

## 📝 Change Log

| วันที่ | เวอร์ชัน | รายละเอียด |
| ------ | -------- | ---------- |
| 2026-03-12 | 2.0 | **Major Update:** Changed from Fullstack project to Insurance OCR POC SPA. Single HTML file, CDN-only, client-side only. Updated all sections. |
| 2026-03-12 | 1.0 | สร้างเอกสาร PRD เริ่มต้น (auto-generated จาก init-ai-workflow) |

