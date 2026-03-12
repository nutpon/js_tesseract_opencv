# 🔄 Hand-over Document (ส่งต่อระหว่าง Session)

> ⚡ **ต้องอัปเดตไฟล์นี้ทุกครั้งก่อนจบ Session**
> ไฟล์นี้คือที่เก็บข้อมูลส่งต่อระหว่าง AI Session หรือระหว่างคนในทีม

---

## 📌 สถานะปัจจุบัน

| หัวข้อ | รายละเอียด |
| ------ | --------- |
| **Project Name** | Insurance OCR POC |
| **Phase ปัจจุบัน** | Phase 3 — Manual Testing with Real Documents (user task) |
| **สถานะรวม** | 🟢 Phase 0, 1, 2 COMPLETE — automated benchmark built-in |
| **อัปเดตล่าสุด** | 2026-03-12 |

---

## ✅ สิ่งที่ทำเสร็จแล้ว

### Phase 0 — Core Implementation (DONE ✅)
- ✅ **index.html** — Single-file SPA created at project root
- ✅ **CDN Libraries loaded** — Tesseract.js v5, OpenCV.js 4.10 (WASM)
- ✅ **File Upload** — Validation (type + size), preview on Canvas 1
- ✅ **OpenCV Processing** — Grayscale + Adaptive / Otsu Threshold → Canvas 2
- ✅ **Tesseract OCR** — Thai+English (`tha+eng`), configurable PSM (1/3/6/11)
- ✅ **Settings Panel** — Threshold method, block size, C constant, PSM mode, language
- ✅ **Status Bar** — Live status with dot indicator
- ✅ **Execution Time** — Displayed after OCR completes
- ✅ **Copy to Clipboard** — Button appears after result
- ✅ **Reset / Repeat** — Clears all; allows re-upload
- ✅ **OpenCV Load Guard** — Start button disabled until `cv` ready
- ✅ **Heavy Comments** — Every section and function documented inline
- ✅ **Dark Theme UI** — Responsive, card-based layout

### Phase 1 — Enhancements & Refinement (DONE ✅)
- ✅ **Drag-and-drop** — Drop zone + click-to-browse; page-level drop prevention
- ✅ **Gaussian Blur** — Optional toggle; 3×3 kernel before thresholding
- ✅ **Morphological Cleanup** — Optional toggle; MORPH_CLOSE 2×2 kernel
- ✅ **Re-process Button** — Change settings and re-run without re-uploading image
- ✅ **Progress Bar** — Animated bar 0-100% synced with Tesseract logger
- ✅ **Timing Breakdown** — Separate badges: OpenCV time, Tesseract time, Total, Character count
- ✅ **Download .txt** — Export OCR result as `{filename}_ocr.txt`
- ✅ **ensureOriginalRendered()** — Re-reads file for Canvas 1 on re-process
- ✅ **renderOriginalImage → Promise** — Now awaitable for pipeline sequencing

### Phase 2 — Automated Benchmark (DONE ✅)
- ✅ **Test image generator** — Canvas 2D renders known English/Thai/Mixed text
- ✅ **5 test cases** — English large/small, Thai large/small, Mixed TH+EN
- ✅ **8 setting combos** — Adaptive/Otsu × Blur × Morph × PSM variations
- ✅ **40 automated runs** — Full matrix: 5 cases × 8 combos
- ✅ **LCS accuracy measurement** — Compares OCR output to expected text
- ✅ **Results table** — Best-per-case row highlighted green
- ✅ **Live benchmark log** — Real-time progress in monospace panel
- ✅ **Export report** — Download full benchmark as `.txt` file
- ✅ **One-click execution** — Just open page, click "Run Full Benchmark"

---

## 🔨 งานที่กำลังทำค้าง (In Progress)

| งาน | สถานะ | รายละเอียด |
| --- | ------ | --------- |
| Run automated benchmark | ⬜ User task | Open index.html → click "Run Full Benchmark" |
| Test with real A4 docs | ⬜ User task | Upload actual insurance policy scans |
| Browser compat test | ⬜ User task | Try Chrome, Firefox, Safari |

---

## 📋 สิ่งที่ต้องทำต่อ (Next Steps)

### Phase 2: Manual Testing
1. Open `index.html` in browser
2. Upload real A4 insurance policy scans
3. For each document, test all combinations:
   - Adaptive vs Otsu threshold
   - Blur ON vs OFF
   - Morph ON vs OFF
   - PSM 1 vs 3 vs 6
4. Record which combo gives best text accuracy
5. Test Thai-only, English-only, and mixed documents
6. Verify on Chrome, Firefox, Safari

### Optional Future Enhancements
- PDF support (via pdf.js)
- Batch processing (multiple files)
- Image zoom/pan on canvas
- Confidence score display per word
- Compare before/after text diff

---

## ⚠️ ปัญหา / Blockers

| ปัญหา | Severity | สถานะ | แนวทางแก้ |
| ----- | --------- | ----- | --------- |
| OpenCV.js WASM loading | 🟡 Medium | ✅ Handled | `onload` callback + status bar; Start disabled until ready |
| Tesseract first load slow | 🟡 Medium | ✅ Handled | Live progress bar + percentage in status bar |
| Thai language accuracy | 🟡 Medium | 🔄 Needs testing | Use Gaussian Blur + tune threshold for Thai docs |

---

## 📎 ไฟล์ที่เกี่ยวข้อง

| ไฟล์ | จุดประสงค์ | สถานะ |
| --- | --------- | ------ |
| `index.html` | Main application (SPA) | ✅ Phase 0 + 1 complete |
| `ai-workflow/prd.md` | Product requirements | ✅ v2.0 |
| `ai-workflow/design-spa.md` | SPA architecture | ✅ Created |
| `ai-workflow/checklist.md` | Progress tracking | ✅ v3.0 (Phase 0+1 done) |
| `ai-workflow/hand-over.md` | This file | ✅ Synced |

---

## 🗒️ Notes / บันทึกเพิ่มเติม

- **index.html is ~950 lines** — fully self-contained single-file SPA
- **Phase 1 additions:** drag-drop, blur, morph, re-process, progress bar, timing breakdown, .txt export
- **OpenCV pipeline is now 4-step:** Grayscale → (optional Blur) → Threshold → (optional Morph)
- **Re-process workflow:** User changes settings → clicks "Re-process" → pipeline re-reads from original canvas
- **All OpenCV matrices are properly freed** after processing (`src.delete()`, `gray.delete()`, etc.)

---

## 📏 วิธีใช้ไฟล์นี้

> **⚡ กฎสำคัญ**: อัปเดตไฟล์นี้ **ทุกครั้ง** ก่อนจบ Session
> 
> **ขั้นตอน:**
> 1. อัปเดต "สิ่งที่ทำเสร็จแล้ว" (✅ section)
> 2. อัปเดต "งานที่กำลังทำค้าง" (🔨 section)
> 3. อัปเดต "ปัญหา/Blockers" (⚠️ section)
> 4. อัปเดต "ไฟล์ที่เกี่ยวข้อง" ถ้ามีไฟล์ใหม่
> 5. Commit เข้า git ก่อนจบ session
