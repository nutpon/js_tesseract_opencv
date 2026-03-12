# ✅ Fullstack Checklist

> Checklist งาน Fullstack stream แยกตาม Phase

---

## Phase 0: Project Setup

- [ ] Create Node.js project (package.json)
- [ ] Set up .gitignore
- [ ] Configure build tool (Webpack or Vite)
- [ ] Create directory structure (src/, public/, tests/)
- [ ] Set up basic HTML boilerplate
- [ ] Install core dependencies (Express, Tesseract.js, OpenCV.js)
- [ ] Document initial setup

---

## Phase 1: Environment & Boilerplate

- [ ] Create Express server with basic routes
- [ ] Set up static file serving (public folder)
- [ ] Create frontend entry point (HTML + CSS)
- [ ] Set up Tesseract.js worker initialization
- [ ] Set up OpenCV.js initialization
- [ ] Create basic API structure
- [ ] Set up logging system
- [ ] Create error handling middleware

---

## Phase 2: Core Features Development

### Upload Feature
- [ ] Create upload API endpoint (/api/upload)
- [ ] Implement file validation (size, type)
- [ ] Create file service for saving uploads
- [ ] Create upload form component (Frontend)

### OCR Feature
- [ ] Create OCR API endpoint (/api/ocr)
- [ ] Implement TesseractService wrapper
- [ ] Create result display component (Frontend)
- [ ] Add language support (Thai, English)
- [ ] Test OCR accuracy

### Image Processing Feature
- [ ] Create image processing API (/api/process-image)
- [ ] Implement OpenCVService wrapper
- [ ] Add preprocessing functions (enhance, detect edges, etc.)
- [ ] Integrate preprocessing with OCR

### Export Feature
- [ ] Create export API endpoint (/api/export)
- [ ] Implement ExportService (TXT, JSON)
- [ ] Add PDF export (optional)
- [ ] Test export functionality

---

## Phase 3: Enhancement & Optimization

- [ ] Performance optimization (caching, compression)
- [ ] Add comprehensive error handling
- [ ] Implement unit tests
- [ ] Implement integration tests
- [ ] Add security measures (input validation, rate limiting)
- [ ] Create user documentation
- [ ] Prepare deployment setup (Docker, etc.)
- [ ] Add logging and monitoring

---

## 📝 Change Log

| วันที่ | เวอร์ชัน | รายละเอียด |
| ------ | -------- | ---------- |
| 2026-03-12 | 1.0 | สร้าง Fullstack Checklist |

