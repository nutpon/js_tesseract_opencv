# 📋 Phase 0: Project Setup — Fullstack

> สำรวจโค้ดปัจจุบัน + เตรียม Environment

---

## 🎯 เป้าหมาย

- ✅ สร้าง Node.js project structure
- ✅ ตั้งค่า Build tool (Webpack / Vite)
- ✅ ติดตั้ง Core dependencies (Tesseract.js, OpenCV.js)
- ✅ สร้าง Frontend boilerplate
- ✅ สร้าง Backend boilerplate
- ✅ โครงสร้าง folder พร้อมใช้

---

## 📋 Tasks

### Task 0.1: Initialize Node.js Project
- [ ] สร้าง `package.json` ด้วย npm init
  ```bash
  npm init -y
  ```
- [ ] สร้าง `.gitignore` (ตัวอย่างด้านล่าง)
  ```
  node_modules/
  dist/
  .env
  .env.local
  .DS_Store
  *.log
  temp/
  uploads/
  ```
- [ ] ตั้งค่า package.json:
  ```json
  {
    "name": "js_tesseract_opencv",
    "version": "1.0.0",
    "description": "JavaScript OCR + Computer Vision",
    "main": "src/index.js",
    "scripts": {
      "start": "node src/index.js",
      "dev": "webpack serve --mode development",
      "build": "webpack --mode production",
      "test": "jest"
    }
  }
  ```

### Task 0.2: Install Core Dependencies
```bash
npm install express
npm install tesseract.js
npm install opencv.js
npm install --save-dev webpack webpack-cli webpack-dev-server
npm install --save-dev jest
```

### Task 0.3: Create Directory Structure
```bash
mkdir -p src/{api,services,utils,frontend}
mkdir -p tests/{unit,e2e}
mkdir -p config
mkdir -p public/images
mkdir -p temp
mkdir -p results
```

### Task 0.4: Create Server Entry Point
**File:** `src/index.js`
```javascript
const express = require('express');
const path = require('path');

const app = express();
const PORT = process.env.PORT || 3000;

// Middleware
app.use(express.json());
app.use(express.static(path.join(__dirname, '../public')));

// Routes
app.get('/', (req, res) => {
  res.sendFile(path.join(__dirname, '../src/frontend/index.html'));
});

// API Routes (to be added)
// app.post('/api/upload', ...);
// app.post('/api/ocr', ...);

// Error handling
app.use((err, req, res, next) => {
  console.error(err);
  res.status(err.statusCode || 500).json({
    status: 'error',
    message: err.message
  });
});

app.listen(PORT, () => {
  console.log(`Server running on http://localhost:${PORT}`);
});
```

### Task 0.5: Create Frontend Boilerplate
**File:** `src/frontend/index.html`
```html
<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>JS Tesseract OpenCV - OCR & Image Processing</title>
  <link rel="stylesheet" href="/styles.css">
</head>
<body>
  <div class="container">
    <header>
      <h1>📄 OCR & Image Processing Tool</h1>
      <p>Extract text from images using Tesseract.js + OpenCV</p>
    </header>

    <main>
      <!-- Upload Section -->
      <section class="upload-section">
        <h2>Step 1: Upload Image</h2>
        <input type="file" id="imageInput" accept="image/*">
        <img id="preview" alt="Image preview" style="max-width: 400px; margin-top: 10px;">
      </section>

      <!-- Processing Section -->
      <section class="processing-section">
        <h2>Step 2: Process Image</h2>
        <button id="extractBtn">🔤 Extract Text (OCR)</button>
        <button id="enhanceBtn">✨ Enhance Image</button>
        <button id="edgesBtn">📐 Detect Edges</button>
      </section>

      <!-- Results Section -->
      <section class="results-section">
        <h2>Step 3: View Results</h2>
        <div id="results" class="results-container"></div>
        <button id="exportBtn" style="display:none;">💾 Export Results</button>
      </section>
    </main>
  </div>

  <script src="app.js"></script>
</body>
</html>
```

**File:** `src/frontend/styles.css`
```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  min-height: 100vh;
  padding: 20px;
}

.container {
  max-width: 1000px;
  margin: 0 auto;
  background: white;
  border-radius: 12px;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.1);
  padding: 40px;
}

header {
  text-align: center;
  margin-bottom: 40px;
}

header h1 {
  color: #333;
  margin-bottom: 10px;
}

header p {
  color: #666;
  font-size: 16px;
}

section {
  margin-bottom: 30px;
  padding: 20px;
  background: #f8f9fa;
  border-radius: 8px;
  border-left: 4px solid #667eea;
}

section h2 {
  margin-bottom: 15px;
  color: #333;
  font-size: 18px;
}

input[type="file"] {
  padding: 10px;
  border: 2px dashed #667eea;
  border-radius: 4px;
  width: 100%;
}

button {
  background: #667eea;
  color: white;
  border: none;
  padding: 10px 20px;
  margin-right: 10px;
  margin-bottom: 10px;
  border-radius: 4px;
  cursor: pointer;
  font-size: 14px;
  transition: background 0.3s;
}

button:hover {
  background: #764ba2;
}

.results-container {
  background: white;
  padding: 15px;
  border-radius: 4px;
  min-height: 100px;
  word-wrap: break-word;
}
```

**File:** `src/frontend/app.js`
```javascript
document.addEventListener('DOMContentLoaded', () => {
  const imageInput = document.getElementById('imageInput');
  const preview = document.getElementById('preview');
  const extractBtn = document.getElementById('extractBtn');
  const enhanceBtn = document.getElementById('enhanceBtn');
  const edgesBtn = document.getElementById('edgesBtn');
  const exportBtn = document.getElementById('exportBtn');
  const resultsDiv = document.getElementById('results');

  let currentImagePath = null;

  // Handle image upload
  imageInput.addEventListener('change', (e) => {
    const file = e.target.files[0];
    if (file) {
      const reader = new FileReader();
      reader.onload = (event) => {
        preview.src = event.target.result;
        // TODO: Upload to server and get path
      };
      reader.readAsDataURL(file);
    }
  });

  // Extract text
  extractBtn.addEventListener('click', async () => {
    if (!currentImagePath) {
      alert('Please upload an image first');
      return;
    }
    
    try {
      extractBtn.disabled = true;
      extractBtn.textContent = '⏳ Processing...';
      
      // TODO: Call /api/ocr endpoint
      resultsDiv.textContent = 'Processing...';
    } catch (error) {
      resultsDiv.textContent = `Error: ${error.message}`;
    } finally {
      extractBtn.disabled = false;
      extractBtn.textContent = '🔤 Extract Text (OCR)';
    }
  });

  // More event listeners to be added...
});
```

### Task 0.6: Create Webpack Configuration
**File:** `config/webpack.config.js`
```javascript
const path = require('path');

module.exports = {
  mode: 'development',
  entry: './src/frontend/app.js',
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, '../public')
  },
  devServer: {
    port: 3000,
    static: {
      directory: path.join(__dirname, '../public')
    }
  }
};
```

### Task 0.7: Create Initial Services
**File:** `src/services/tesseract-service.js`
```javascript
const Tesseract = require('tesseract.js');

class TesseractService {
  constructor() {
    this.worker = null;
  }

  async initialize(language = 'eng+tha') {
    if (!this.worker) {
      this.worker = await Tesseract.createWorker(language);
    }
  }

  async recognizeImage(imagePath) {
    // TODO: Implement
  }

  async terminate() {
    if (this.worker) {
      await this.worker.terminate();
      this.worker = null;
    }
  }
}

module.exports = TesseractService;
```

**File:** `src/services/file-service.js`
```javascript
const fs = require('fs').promises;
const path = require('path');

class FileService {
  constructor(tempDir = 'temp') {
    this.tempDir = tempDir;
  }

  async saveUploadedFile(file) {
    // TODO: Implement
  }

  async deleteFile(filePath) {
    // TODO: Implement
  }
}

module.exports = FileService;
```

---

## 📚 Resources / References

- [Express.js Documentation](https://expressjs.com)
- [Tesseract.js Documentation](https://github.com/naptha/tesseract.js)
- [OpenCV.js Documentation](https://docs.opencv.org/4.4.0/d5/d10/tutorial_js_root.html)
- [Webpack Documentation](https://webpack.js.org)

---

## ⚠️ Risks / Considerations

1. **WASM Module Loading:** Tesseract.js and OpenCV.js ใช้ WASM ต้องแน่ใจว่า browser รองรับ
2. **Memory Usage:** WASM modules อาจใช้ memory มาก ต้อง optimize
3. **Dependency Compatibility:** ต้องตรวจสอบ version compatibility ระหว่าง libraries
4. **Build Performance:** WASM bundling อาจทำให้ build time นาน

---

## 📝 Change Log

| วันที่ | เวอร์ชัน | รายละเอียด |
| ------ | -------- | ---------- |
| 2026-03-12 | 1.0 | สร้าง Phase 0 plan |

