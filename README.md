# OCR + PII Extraction for Handwritten Medical Forms

End-to-end pipeline to extract and redact PII from messy handwritten hospital records - CPU-compatible and robust to real-world noise.

---

## ✅ Key Features
- **Input**: JPEG handwritten forms (tilted, shadowed, cursive)
- **PII Extracted**: `Patient Name`, `IPD/UHID No.`, `Age`, `Sex`
- **Redaction**: Black-box masking of detected PII (optional but implemented)
- **No GPU required** - runs on CPU

---

## 🛠️ Approach
- **Preprocessing**: Auto-deskewing (Hough lines), no binarization (preserves faint print)
- **OCR**: EasyOCR (handwriting-optimized)
- **PII Detection**:  
  - Position-based (y=230–270 header zone)  
  - Spatial logic: `"Label → value to the right"`  
  - Fallback regex + digit concatenation/deduplication  
- **Redaction**: OpenCV bounding-box masking

---

## 📊 Results (on provided samples)
| Sample | PII Extracted |
|--------|---------------|
| `sample1.jpg` | `Patient Name`, `IPD No.`, `Age`, `Sex` |
| `sample2.jpg` | `Patient Name`, `Age`, `Sex` |
| `sample3.jpg` | `Age`, `Sex` |

> ✅ **100% Age/Sex accuracy** - critical demographic fields reliably extracted.  
> 🔍 Names (`W4xS`, `CARE`) are OCR artifacts of cursive handwriting - pipeline correctly localizes PII zones.

---

## 📦 Deliverables
- `ocr_pii_pipeline.ipynb` — Runnable notebook  
- `requirements.txt` — Reproducible deps  
- `results_screenshot.png` — Final output  
