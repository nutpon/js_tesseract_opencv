# 📁 Project Structure

> โครงสร้าง Folder และ File ทั้งหมดของโปรเจกต์ **Insurance OCR POC**
> 📌 ไฟล์หลัก: `index.html` (ไฟล์เดียว ที่มี HTML, CSS, JavaScript ทั้งหมด)

---

## 🌐 Root Directory

```
js_tesseract_opencv/                    # Project root
├── .git/                               # Git repository
├── .gitignore                          # Git ignore rules
├── .idea/                              # IDE configuration (JetBrains)
├── README.md                           # Project README
├── init-ai-workflow.md                 # AI Workflow initialization guide
│
├── index.html                          # 🚀 MAIN APPLICATION FILE
│                                       # Single HTML file containing:
│                                       # - HTML structure (input, canvas, textarea)
│                                       # - Embedded CSS styling
│                                       # - Embedded JavaScript code
│
├── ai-workflow/                        # 📋 AI Workflow Documentation
│   ├── start-up.md                     # 🚀 Onboarding guide
│   ├── prd.md                          # 📋 Product Requirements (v2.0)
│   ├── hand-over.md                    # 🔄 Session progress tracking
│   ├── structure-file.md               # 📁 This file - directory mapping
│   ├── principle.md                    # 📐 Standards & conventions
│   ├── checklist.md                    # ✅ Overall project progress
│   ├── design-fullstack.md             # 🎨 Old fullstack design (deprecated)
│   ├── design-spa.md                   # 🎨 NEW - SPA architecture document
│   ├── issue-log.md                    # 🐛 Bug tracker
│   ├── impact-analysis.md              # 🔍 Change impact map
│   ├── README.md                       # Workflow master guide
│   ├── QUICK-START.md                  # Quick start guide
│   ├── QUICK-REFERENCE.md              # Quick reference
│   ├── INDEX.md                        # File index & navigation
│   │
│   └── implement-plan-fullstack/       # 📂 Legacy folder (for reference)
│       ├── hand-over.md                # (kept for historical record)
│       ├── checklist.md                # (kept for historical record)
│       └── phase-00.md                 # (kept for historical record)
│
└── public/                             # 📦 Optional: Static assets (if needed)
    ├── images/                         # Example images for testing
    └── favicon.ico                     # Website favicon (optional)
```

---

## 📊 Directory Size Estimate

| Directory | Purpose | Size (est.) |
| --------- | ------- | ----------- |
| `index.html` | Main application | ~100-300 KB |
| `ai-workflow/` | Documentation | ~500 KB |
| `.git/` | Version control | ~1 MB |
| **Total** | | **~2 MB** |

---

## 📝 File Descriptions

### Root Level Files

| File | Purpose | Size |
| ---- | ------- | ---- |
| **index.html** | Single-page application with embedded CSS & JS | ~100-300 KB |
| **README.md** | Project overview and instructions | ~2 KB |
| **init-ai-workflow.md** | AI Workflow initialization notes | ~35 KB |

### ai-workflow/ Documentation

| File | Purpose | Status |
| ---- | ------- | ------ |
| **prd.md** | Product Requirements (v2.0) | ✅ Updated |
| **design-spa.md** | SPA Architecture | ✅ NEW |
| **design-fullstack.md** | Old Fullstack Design | ⚠️ Deprecated |
| **start-up.md** | Onboarding guide | ✅ Current |
| **hand-over.md** | Session tracking | ✅ Updated |
| **structure-file.md** | This file | ✅ Updated |
| **principle.md** | Standards & conventions | ⚠️ Needs vanilla JS update |
| **README.md** | Workflow master guide | ✅ Current |
| **QUICK-START.md** | 30-second quick start | ✅ Current |

---

## 🔄 Key Changes from Fullstack to SPA

### BEFORE (Fullstack Structure)
```
src/
├── index.js
├── api/
├── services/
├── utils/
└── frontend/
    └── index.html
```

### AFTER (Single HTML SPA)
```
index.html  (ONE FILE with everything)
```

---

## 🚀 How Files Are Organized

### By Role

**For Developers:**
- `index.html` - The code you'll edit
- `ai-workflow/design-spa.md` - Architecture reference
- `ai-workflow/principle.md` - Coding guidelines (vanilla JS)
- `ai-workflow/prd.md` - Feature requirements

**For Managers/Leads:**
- `ai-workflow/hand-over.md` - Project status
- `ai-workflow/checklist.md` - Progress tracking
- `ai-workflow/prd.md` - Feature list

**For Documentation:**
- `ai-workflow/` - All markdown docs
- `README.md` - Quick overview

---

## 📝 Change Log

| วันที่ | เวอร์ชัน | รายละเอียด |
| ------ | -------- | ---------- |
| 2026-03-12 | 2.0 | Updated structure for Insurance OCR POC - Single HTML file at root level |
| 2026-03-12 | 1.0 | สร้างโครงสร้างไฟล์เริ่มต้น (fullstack) |

> **หมายเหตุ:** อัปเดตไฟล์นี้ทุกครั้งที่มีการเพิ่ม/ลบ folder หรือ file ใหม่

