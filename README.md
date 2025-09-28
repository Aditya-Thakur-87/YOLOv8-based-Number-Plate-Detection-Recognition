# YOLOv8-based Number Plate Detection & Recognition

## Overview
This project implements **Automatic Number Plate Recognition (ANPR)** for both **Indian** and **UK** license plates using:
- **YOLOv8** for vehicle & plate detection
- **Tesseract OCR** with EasyOCR fallback for text recognition
- **SORT tracker** to assign plates to vehicles
- **SQLite** for structured result storage

Supports:
- Indian plates (`LLDDLLDDDD`, e.g., KA02MN1826)
- UK plates (`AANNAAA`, e.g., AB12CDE)

---

## Features
- Train YOLOv8 on Roboflow datasets
- Detect vehicles and number plates from video
- OCR with Tesseract → EasyOCR fallback → raw text fallback
- Plate format correction rules (India/UK specific)
- Vehicle-to-plate assignment using SORT
- Confidence visualization (green/orange/red)
- Cropped plate saving for debugging
- SQLite integration + summary filtering

---

## Pipeline
1. **Detection**: YOLOv8 finds vehicles and plates.
2. **Tracking**: SORT assigns unique IDs to vehicles.
3. **OCR**: Preprocessing → Tesseract → EasyOCR → fallback.
4. **Correction**: Format-specific cleanup of OCR results.
5. **Visualization**: Plates drawn with color-coded confidence.
6. **Database**: All results stored in SQLite with summary option.

---

## Installation
```bash
# Install dependencies
pip install ultralytics==8.3.203 easyocr pytesseract opencv-python filterpy roboflow
sudo apt-get install -y tesseract-ocr libtesseract-dev
```

---

## Usage
1. **Train YOLOv8 on plates**
   ```python
   from ultralytics import YOLO
   model = YOLO("yolov8s.pt")
   model.train(data="data.yaml", epochs=50, imgsz=960)
   ```

2. **Run ANPR pipeline**
   ```python
   run_npr("input_video.mp4", "output_dir/")
   ```

3. **Summarize results**
   ```python
   summarize_and_save("plates.db", "plates_summary.db")
   ```

---

## Outputs
- Annotated video (`.mp4`)
- Raw detections DB (`plates.db`)
- Clean summary DB (`plates_summary.db`)

---

