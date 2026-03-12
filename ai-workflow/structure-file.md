# 📁 Project Structure

> โครงสร้าง Folder และ File ทั้งหมดของโปรเจกต์ js_tesseract_opencv

---

## 🌐 Root Directory

```
js_tesseract_opencv/                    # Project root
├── .git/                               # Git repository
├── .gitignore                          # Git ignore rules
├── .idea/                              # IDE configuration (JetBrains)
├── package.json                        # Node.js project metadata & dependencies
├── package-lock.json                   # Dependency lock file
├── .env.example                        # Environment variables template
├── README.md                           # Project README
├── init-ai-workflow.md                 # AI Workflow initialization guide
│
├── ai-workflow/                        # 📋 AI Workflow Documentation
│   ├── start-up.md                     # Onboarding guide
│   ├── prd.md                          # Product Requirements Document
│   ├── hand-over.md                    # Session hand-over document
│   ├── structure-file.md               # This file - directory mapping
│   ├── principle.md                    # Documentation & coding standards
│   ├── checklist.md                    # Overall progress tracking
│   ├── design-fullstack.md             # Architecture & design document
│   ├── issue-log.md                    # Bug & issue tracker
│   ├── impact-analysis.md              # Change impact analysis
│   │
│   └── implement-plan-fullstack/       # Implementation plan for fullstack
│       ├── hand-over.md                # Stream-specific hand-over
│       ├── checklist.md                # Stream-specific progress
│       ├── phase-00.md                 # Phase 0: Project Setup
│       ├── phase-01.md                 # Phase 1: Environment & Boilerplate
│       ├── phase-02.md                 # Phase 2: Core Features
│       └── phase-03.md                 # Phase 3: Enhancement & Optimization
│
├── src/                                # 📁 Source code
│   ├── index.js                        # Application entry point
│   ├── config.js                       # Configuration settings
│   │
│   ├── api/                            # 🔌 Backend API endpoints
│   │   ├── upload.js                   # Image upload handler
│   │   ├── ocr.js                      # OCR processing
│   │   ├── image-processor.js          # OpenCV image processing
│   │   └── export.js                   # Results export handler
│   │
│   ├── services/                       # 🛠️ Business logic
│   │   ├── tesseract-service.js        # Tesseract.js wrapper
│   │   ├── opencv-service.js           # OpenCV.js wrapper
│   │   ├── file-service.js             # File handling utilities
│   │   └── export-service.js           # Export functionality
│   │
│   ├── utils/                          # 🔧 Utility functions
│   │   ├── validators.js               # Input validation
│   │   ├── converters.js               # Data conversion utilities
│   │   └── logger.js                   # Logging utilities
│   │
│   └── frontend/                       # 🎨 Frontend (Browser UI)
│       ├── index.html                  # Main HTML file
│       ├── styles.css                  # Styling
│       ├── app.js                      # Frontend application logic
│       └── components/                 # UI Components
│           ├── upload-form.js
│           ├── result-display.js
│           └── settings-panel.js
│
├── tests/                              # 🧪 Test files
│   ├── unit/                           # Unit tests
│   │   ├── tesseract-service.test.js
│   │   ├── opencv-service.test.js
│   │   └── validators.test.js
│   │
│   └── e2e/                            # End-to-end tests
│       └── main-flow.test.js
│
├── config/                             # ⚙️ Configuration files
│   ├── webpack.config.js               # Webpack configuration
│   ├── jest.config.js                  # Jest testing configuration
│   └── .env.example                    # Environment variables template
│
├── docs/                               # 📚 Additional documentation
│   ├── API.md                          # API specification
│   ├── INSTALLATION.md                 # Setup & installation guide
│   ├── USAGE.md                        # Usage guide
│   └── TROUBLESHOOTING.md              # Troubleshooting guide
│
└── public/                             # 📦 Static assets
    ├── images/                         # Example images for testing
    ├── icons/                          # App icons
    └── favicon.ico                     # Website favicon
```

---

## 📊 Directory Size Estimate

| Directory | Purpose | Size (est.) |
| --------- | ------- | ----------- |
| `src/` | Source code | ~500KB |
| `node_modules/` | Dependencies | ~500MB |
| `ai-workflow/` | Documentation | ~500KB |
| `tests/` | Test files | ~200KB |
| `public/` | Static assets | ~5MB |
| **Total** | | **~505MB** |

---

## 🔄 Key Relationships

### Dependencies Between Directories

```
frontend (src/frontend/)
    ↓ calls
api (src/api/)
    ↓ calls
services (src/services/)
    ├─ tesseract-service → node_modules/tesseract.js
    └─ opencv-service → node_modules/opencv.js

tests/ → src/ (testing all modules)
```

---

## 📝 Change Log

| วันที่ | เวอร์ชัน | รายละเอียด |
| ------ | -------- | ---------- |
| 2026-03-12 | 1.0 | สร้างโครงสร้างไฟล์เริ่มต้น |

> **หมายเหตุ:** อัปเดตไฟล์นี้ทุกครั้งที่มีการเพิ่ม/ลบ folder หรือ file ใหม่

