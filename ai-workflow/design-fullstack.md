# 🎨 Design — Single-Page Application (SPA)

> เอกสารออกแบบระบบสำหรับ **Insurance OCR POC**
> ครอบคลุม: Client-Side Only Architecture, Processing Pipeline, UI Components

---

## 1. 🏗️ Architecture Overview

### 1.1 High-Level Architecture (Client-Side Only)

```
┌─────────────────────────────────────────────────────────────┐
│                    Browser (Client-Side)                     │
│  ┌──────────────────────────────────────────────────────┐   │
│  │  index.html (Single HTML File)                       │   │
│  │  ├─ HTML Structure                                   │   │
│  │  ├─ Embedded CSS Styling                             │   │
│  │  └─ Embedded JavaScript                              │   │
│  └──────────────────────────────────────────────────────┘   │
│                          ↓                                    │
│  ┌──────────────────────────────────────────────────────┐   │
│  │  UI Layer (HTML Elements)                            │   │
│  │  ├─ Input Section (File upload, buttons)             │   │
│  │  ├─ Canvas 1 (Original image display)                │   │
│  │  ├─ Canvas 2 (Processed image display)               │   │
│  │  └─ Output Section (Textarea, status, timing)        │   │
│  └──────────────────────────────────────────────────────┘   │
│                          ↓                                    │
│  ┌──────────────────────────────────────────────────────┐   │
│  │  Processing Logic Layer (JavaScript Functions)       │   │
│  │  ├─ uploadHandler() - Handle file selection          │   │
│  │  ├─ processImage() - Orchestrate pipeline            │   │
│  │  ├─ opencvProcess() - Image preprocessing            │   │
│  │  ├─ tesseractOCR() - Text extraction                 │   │
│  │  └─ updateUI() - Display results & status            │   │
│  └──────────────────────────────────────────────────────┘   │
│                          ↓                                    │
│  ┌──────────────────────────────────────────────────────┐   │
│  │  CDN Libraries (Loaded via Script Tags)              │   │
│  │  ├─ OpenCV.js (Image processing)                     │   │
│  │  └─ Tesseract.js (OCR extraction)                    │   │
│  └──────────────────────────────────────────────────────┘   │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

### 1.2 Technology Stack

| Layer | Technology | Purpose |
| ----- | ---------- | ------- |
| **Container** | Single HTML File | Self-contained, portable |
| **Markup** | HTML5 | Document structure |
| **Styling** | CSS3 (embedded) | Layout and appearance |
| **Logic** | Vanilla JavaScript | Event handling, coordination |
| **Image Processing** | OpenCV.js (CDN) | Pre-processing: grayscale, thresholding |
| **OCR** | Tesseract.js (CDN) | Text extraction with Thai+English |
| **Deployment** | Browser only | No server, no build tools |
│  │  ├─ tesseract.js (WASM OCR)                          │   │
│  │  └─ opencv.js (WASM Computer Vision)                 │   │
│  └──────────────────────────────────────────────────────┘   │
│                          ↓                                    │
│  ┌──────────────────────────────────────────────────────┐   │
│  │  Storage                                             │   │
│  │  ├─ Temp folder (uploaded files)                     │   │
│  │  └─ Results folder (export files)                    │   │
│  └──────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
```

### 1.2 Technology Stack

| Layer | Technology | Purpose |
| ----- | ---------- | ------- |
| **Frontend** | HTML5 + CSS3 + Vanilla JS | User interface |
| **Frontend Build** | Webpack / Vite | Module bundling |
| **Backend Runtime** | Node.js 18+ | Server runtime |
| **Web Framework** | Express.js | HTTP server |
| **OCR** | Tesseract.js 4.x | WASM-based OCR |
| **CV** | OpenCV.js 4.x | WASM-based image processing |
| **Testing** | Jest | Unit & integration tests |
| **Build Tool** | Webpack / Vite | Build bundler |

---

## 2. 📁 Project Structure

```
src/
├── index.js                          # Server entry point
├── config.js                         # Configuration
├── api/                              # API routes
│   ├── upload.js                     # POST /api/upload
│   ├── ocr.js                        # POST /api/ocr
│   ├── image-processor.js            # POST /api/process-image
│   └── export.js                     # POST /api/export
├── services/                         # Business logic
│   ├── tesseract-service.js          # Tesseract.js wrapper
│   ├── opencv-service.js             # OpenCV.js wrapper
│   ├── file-service.js               # File handling
│   └── export-service.js             # Export functionality
├── utils/                            # Utilities
│   ├── validators.js                 # Input validation
│   ├── converters.js                 # Data conversion
│   └── logger.js                     # Logging
├── frontend/                         # Frontend code
│   ├── index.html                    # Main HTML
│   ├── styles.css                    # CSS styling
│   ├── app.js                        # Frontend app
│   └── components/                   # UI components
│       ├── upload-form.js
│       ├── result-display.js
│       └── settings-panel.js
└── public/                           # Static assets
    └── images/                       # Test images
```

---

## 3. 🎨 Design Convention

### 3.1 Naming Convention

#### JavaScript Files & Folders
- **Folders:** kebab-case: `api/`, `services/`, `utils/`
- **Service files:** kebab-case + `-service.js`: `tesseract-service.js`, `file-service.js`
- **API handlers:** kebab-case: `upload.js`, `ocr.js`
- **Classes:** PascalCase: `TesseractService`, `OpenCVService`
- **Functions:** camelCase: `processImage()`, `extractText()`
- **Constants:** UPPER_SNAKE_CASE: `MAX_FILE_SIZE`, `TEMP_FOLDER`

#### API Naming
- **Routes:** kebab-case: `/api/upload`, `/api/ocr`, `/api/process-image`
- **Methods:** POST for operations, GET for retrieval
- **Response format:** JSON with status, data, error fields

```javascript
// ✅ Correct response format
{
  status: "success",      // or "error"
  data: { ... },          // actual result
  message: "Text extracted successfully"
}

// ❌ Incorrect
{ success: true, result: ... }
```

### 3.2 Folder Structure Convention

```
api/            → HTTP handlers (request/response)
services/       → Business logic (Tesseract, OpenCV wrapper)
utils/          → Helper functions (validators, converters)
frontend/       → Browser-side code (HTML, CSS, JS)
```

### 3.3 Code Style

#### JavaScript Style Guide

- **Indentation:** 2 spaces
- **Semicolons:** Always use
- **Quotes:** Single quotes for strings
- **Async/Await:** Prefer over `.then()` chains
- **Error handling:** Try-catch blocks with meaningful messages

```javascript
// ✅ Correct
async function extractText(imagePath) {
  try {
    const worker = await Tesseract.createWorker();
    const result = await worker.recognize(imagePath);
    return result.data.text;
  } catch (error) {
    logger.error(`OCR failed: ${error.message}`);
    throw new Error('Failed to extract text from image');
  }
}

// ❌ Avoid
function extractText(imagePath) {
  return tesseract.recognize(imagePath).then(r => r.data.text);
}
```

### 3.4 File Size Limits

- **Max file size for upload:** 5MB
- **Max image dimensions:** 4096x4096 pixels
- **Supported formats:** JPG, PNG, GIF, BMP

### 3.5 Error Handling

- Use custom error classes
- Provide meaningful error messages
- Log errors with timestamp and context

```javascript
class ValidationError extends Error {
  constructor(message) {
    super(message);
    this.name = 'ValidationError';
    this.statusCode = 400;
  }
}
```

---

## 4. 📦 Key Components / Modules

### 4.1 Frontend Components

#### UploadForm Component
- **Purpose:** Handle image file upload
- **Inputs:** File input, submit button
- **Outputs:** Emit event to parent with file data
- **Validation:** File type, file size

#### ResultDisplay Component
- **Purpose:** Show OCR results
- **Inputs:** OCR result data
- **Outputs:** Allow copy, export, download
- **Display:** Formatted text with confidence scores

#### SettingsPanel Component
- **Purpose:** Configure processing options
- **Inputs:** Language selection, processing options
- **Outputs:** Settings object to parent
- **Options:** Language (Thai, English), preprocessing options

### 4.2 Backend Services

#### TesseractService
```javascript
class TesseractService {
  async initialize(language = 'eng+tha') { }
  async recognizeImage(imagePath) { }
  async recognizeBuffer(imageBuffer) { }
  async terminate() { }
}
```

#### OpenCVService
```javascript
class OpenCVService {
  async enhanceImage(imagePath) { }
  async detectEdges(imagePath) { }
  async detectContours(imagePath) { }
  async preprocessImage(imagePath) { }
}
```

#### FileService
```javascript
class FileService {
  async saveUploadedFile(file) { }
  async readFile(filePath) { }
  async deleteFile(filePath) { }
  async listFiles(folderPath) { }
}
```

#### ExportService
```javascript
class ExportService {
  async exportToTxt(data, filePath) { }
  async exportToJson(data, filePath) { }
  async exportToPdf(data, filePath) { }  // Optional
}
```

### 4.3 API Endpoints

#### POST /api/upload
- **Purpose:** Upload image file
- **Input:** File (multipart/form-data)
- **Output:** File ID, filename, size
- **Validation:** File type, file size

#### POST /api/ocr
- **Purpose:** Perform OCR on image
- **Input:** File ID or image path, language
- **Output:** Extracted text, confidence scores
- **Processing:** Call TesseractService

#### POST /api/process-image
- **Purpose:** Preprocess image
- **Input:** File ID, processing options
- **Output:** Processed image (as base64 or file path)
- **Processing:** Call OpenCVService

#### POST /api/export
- **Purpose:** Export results
- **Input:** Result data, format (txt/json/pdf)
- **Output:** File download or data
- **Processing:** Call ExportService

---

## 5. 🔄 Data Flow

### Upload & OCR Flow
```
User selects file
    ↓
UploadForm submits → POST /api/upload
    ↓
FileService saves → Temp folder
    ↓
Return file ID → Frontend
    ↓
User clicks "Extract"
    ↓
POST /api/ocr (file ID)
    ↓
TesseractService.recognize()
    ↓
Return text + confidence → Frontend
    ↓
ResultDisplay shows result
```

### Image Processing Flow
```
User uploads image
    ↓
User clicks "Enhance"
    ↓
POST /api/process-image (file ID, options)
    ↓
OpenCVService.enhance() / .detectEdges() etc.
    ↓
Return processed image (base64) → Frontend
    ↓
User can run OCR on processed image
```

---

## 6. ⚡ Performance Considerations

### OCR Performance
- **For small images (<1MB):** ~2-5 seconds
- **For large images (5MB):** ~10-15 seconds
- **Worker initialization:** ~3-5 seconds (one-time)

### Optimization Strategies
- Cache Tesseract worker instance
- Implement image preprocessing to improve accuracy
- Use Web Workers for long-running operations
- Compress large files before processing

### Browser Compatibility
- Chrome 60+
- Firefox 55+
- Safari 12+
- Edge 79+

---

## 7. 🔐 Security Considerations

- Validate file uploads (type, size)
- Sanitize file names
- Store uploaded files outside web root
- Implement rate limiting for API endpoints
- Validate user input (language codes, etc.)

---

## 📝 Change Log

| วันที่ | เวอร์ชัน | รายละเอียด |
| ------ | -------- | ---------- |
| 2026-03-12 | 1.0 | สร้างเอกสาร Design เริ่มต้น |

