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

---

## 2. 📁 File Structure

Single index.html file with 3 embedded sections:

```html
<!DOCTYPE html>
<html>
<head>
  <!-- Embedded CSS -->
  <style>
    /* ...all styling... */
  </style>
</head>
<body>
  <!-- HTML Structure -->
  <!-- Input Section, Canvas 1 & 2, Output Section -->
  
  <!-- CDN Script Loads -->
  <script src="https://cdn.jsdelivr.net/npm/tesseract.js"></script>
  <script src="https://docs.opencv.org/4.5.0/opencv.js"></script>
  
  <!-- Embedded JavaScript -->
  <script>
    // All processing logic here
  </script>
</body>
</html>
```

---

## 3. 🎨 Design Convention (Vanilla JS)

### 3.1 JavaScript Function Naming

- **Event Handlers:** `handle{Event}()` - e.g., `handleUpload()`, `handleProcess()`
- **Processing Functions:** `process{Name}()` - e.g., `processImage()`, `processOpenCV()`
- **UI Updates:** `update{Section}()` - e.g., `updateStatus()`, `updateCanvases()`
- **Utility Functions:** `{action}{Object}()` - e.g., `getImageFile()`, `renderCanvas()`
- **Global State:** Use simple `let` variables at top of script, clearly commented

### 3.2 Code Organization (Single File)

```javascript
// ========================================
// 1. GLOBAL VARIABLES & CONFIGURATION
// ========================================
let imageFile = null;
let cvReady = false;
let startTime = 0;

const CONFIG = {
  MAX_FILE_SIZE: 5 * 1024 * 1024,  // 5MB
  SUPPORTED_FORMATS: ['jpg', 'jpeg', 'png', 'gif', 'bmp'],
  CANVAS_MAX_WIDTH: 800,
  CANVAS_MAX_HEIGHT: 600
};

// ========================================
// 2. INITIALIZATION FUNCTIONS
// ========================================
function initializeOpenCV() { ... }
function initializeTesseract() { ... }
function setupEventListeners() { ... }

// ========================================
// 3. EVENT HANDLERS
// ========================================
function handleUpload() { ... }
function handleProcessing() { ... }
function handleReset() { ... }

// ========================================
// 4. PROCESSING PIPELINE
// ========================================
function processImage() { ... }
function applyOpenCVProcessing() { ... }
function performTesseractOCR() { ... }

// ========================================
// 5. UI UPDATE FUNCTIONS
// ========================================
function updateStatus(message) { ... }
function updateCanvases(original, processed) { ... }
function displayResults(text) { ... }

// ========================================
// 6. UTILITY FUNCTIONS
// ========================================
function validateFile(file) { ... }
function getImageDimensions(img) { ... }
function calculateExecutionTime() { ... }

// ========================================
// 7. MAIN INITIALIZATION
// ========================================
document.addEventListener('DOMContentLoaded', () => {
  initializeOpenCV();
  setupEventListeners();
});
```

### 3.3 Vanilla JS Best Practices for Single File

- **No external dependencies** beyond CDN libraries
- **Heavy comments** for clarity and maintainability
- **Clear variable names** - no abbreviations
- **Simple data structures** - objects and arrays only
- **Try-catch blocks** for all async operations
- **Console logging** for debugging

### 3.4 Canvas & Image Handling

```javascript
// ✅ Correct Canvas usage
const canvas = document.getElementById('originalCanvas');
const ctx = canvas.getContext('2d');
ctx.drawImage(img, 0, 0, canvas.width, canvas.height);

// ✅ Correct OpenCV usage
const src = cv.imread('originalCanvas');
const gray = new cv.Mat();
cv.cvtColor(src, gray, cv.COLOR_RGBA2GRAY);
cv.imshow('processedCanvas', gray);
src.delete();
gray.delete();
```

---

## 4. 📦 Key Functions / Components

### 4.1 HTML Structure

```html
<!-- Input Section -->
<div id="inputSection">
  <input type="file" id="imageInput" accept="image/*">
  <button id="startBtn">Start Processing</button>
  <button id="resetBtn">Reset</button>
</div>

<!-- Process Pipeline (Canvas Section) -->
<div id="pipelineSection">
  <canvas id="originalCanvas"></canvas>
  <canvas id="processedCanvas"></canvas>
</div>

<!-- Output Section -->
<div id="outputSection">
  <textarea id="resultText" readonly></textarea>
  <div id="status">Waiting...</div>
  <span id="execTime">0.00s</span>
</div>
```

### 4.2 JavaScript Core Functions

#### 1. File Upload Handler
```javascript
function handleUpload() {
  // Get file from input
  // Validate file type/size
  // Read file as image
  // Display on Canvas 1
  // Reset output area
}
```

#### 2. OpenCV Processing
```javascript
function applyOpenCVProcessing(sourceCanvasId, targetCanvasId) {
  // Read image from source canvas
  // Convert to grayscale: cv.cvtColor()
  // Apply thresholding: cv.adaptiveThreshold() or cv.threshold()
  // Display on target canvas
  // Clean up OpenCV matrices
}
```

#### 3. Tesseract OCR
```javascript
function performTesseractOCR(canvasId) {
  // Initialize Tesseract worker with 'tha+eng'
  // Set PSM mode (1 or 3)
  // Run recognition on canvas image
  // Update status with progress
  // Display results
  // Terminate worker
}
```

#### 4. Status Updates
```javascript
function updateStatus(stage, progress) {
  // Loading OpenCV... (0%)
  // Pre-processing... (25%)
  // Running OCR... (75%)
  // Complete! (100%)
}
```

### 4.3 Key Configuration Values

| Setting | Value | Tweakable |
| ------- | ----- | --------- |
| **Grayscale conversion** | cv.COLOR_RGBA2GRAY | ✓ Easy change |
| **Thresholding type** | ADAPTIVE or OTSU | ✓ Easy switch |
| **Threshold block size** | 11 | ✓ Easy tweak |
| **Threshold constant** | 2 | ✓ Easy tweak |
| **Tesseract language** | tha+eng | ✓ Easy change |
| **Tesseract PSM** | 1 or 3 | ✓ Easy switch |

---

## 5. 🔄 Processing Pipeline

### Flow Diagram
```
User uploads file
      ↓
[File Validation]
      ↓
[Render Canvas 1: Original]
      ↓
[OpenCV: Grayscale Conversion]
      ↓
[OpenCV: Apply Thresholding]
      ↓
[Render Canvas 2: Processed]
      ↓
[Tesseract: Initialize Worker]
      ↓
[Tesseract: Run OCR (tha+eng)]
      ↓
[Extract Text & Confidence]
      ↓
[Display Results in Textarea]
      ↓
[Calculate & Show Execution Time]
```

---

## 6. ⚡ Performance Considerations

### Load Times (First Run)
- **OpenCV.js WASM load:** 3-5 seconds
- **Tesseract.js WASM load:** 5-10 seconds
- **Total first run:** 8-15 seconds

### Processing Times (Subsequent Runs)
- **A4 Image processing:** < 1 second
- **OCR extraction:** 3-5 seconds
- **Total per image:** 3-6 seconds

### Optimization Tips
- Show loading indicators during WASM loads
- Cache Tesseract worker after first initialization
- Use canvas for rendering (faster than DOM)
- Handle memory cleanup (delete() OpenCV matrices)

---

## 7. 🔐 Error Handling

### Common Errors to Handle

1. **OpenCV not loading** - Show error, disable processing button
2. **File upload issues** - Validate type/size, show user message
3. **Tesseract OOM** - Handle gracefully, inform user
4. **Canvas rendering issues** - Fallback messaging
5. **Invalid image data** - Try-catch with user feedback

---

## 📝 Change Log

| วันที่ | เวอร์ชัน | รายละเอียด |
| ------ | -------- | ---------- |
| 2026-03-12 | 1.0 | สร้างเอกสาร Design สำหรับ Single-Page SPA (Insurance OCR POC) |

