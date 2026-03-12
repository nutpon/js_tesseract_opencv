# 📋 Phase 1: Core Features Development — Fullstack

> โปรแกรมการพัฒนา Feature หลัก (OCR, Image Processing, Export)

---

## 🎯 เป้าหมาย

- ✅ Implement Image Upload API
- ✅ Implement OCR Text Extraction (Tesseract.js)
- ✅ Implement Image Processing (OpenCV.js)
- ✅ Implement Results Export (TXT, JSON)
- ✅ Create Frontend UI Components
- ✅ Test all features end-to-end

---

## 📋 Tasks

### Upload Feature

- [ ] Create `/api/upload` endpoint
  - File validation (size, type)
  - Save to temp folder
  - Return file metadata
- [ ] Implement FileService.saveUploadedFile()
- [ ] Create upload form component
- [ ] Test file upload

### OCR Feature

- [ ] Create `/api/ocr` endpoint
  - Receive file path / ID
  - Call TesseractService.recognize()
  - Return extracted text + confidence
- [ ] Implement TesseractService
  - Initialize worker with language
  - Process image
  - Parse results
- [ ] Create result display component
- [ ] Add language support (Thai, English)
- [ ] Test OCR accuracy

### Image Processing Feature

- [ ] Create `/api/process-image` endpoint
  - Receive file path + options
  - Call OpenCVService
  - Return processed image
- [ ] Implement OpenCVService
  - Image enhancement
  - Edge detection
  - Contour detection
- [ ] Create processing options UI
- [ ] Test image processing

### Export Feature

- [ ] Create `/api/export` endpoint
  - Receive result + format
  - Call ExportService
  - Return file / data
- [ ] Implement ExportService
  - TXT export
  - JSON export
  - PDF export (optional)
- [ ] Create export UI
- [ ] Test all export formats

### Testing

- [ ] Unit tests for services
- [ ] Integration tests for API
- [ ] E2E tests for workflows

---

## 📚 Resources

- Tesseract.js: https://github.com/naptha/tesseract.js
- OpenCV.js: https://docs.opencv.org/4.4.0/d5/d10/tutorial_js_root.html
- Express.js: https://expressjs.com

---

## 📝 Change Log

| วันที่ | เวอร์ชัน | รายละเอียด |
| ------ | -------- | ---------- |
| 2026-03-12 | 1.0 | สร้าง Phase 1 plan |

