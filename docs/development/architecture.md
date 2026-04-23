# Architecture

## Technology Stack

- **PySide6** - Cross-platform GUI
- **qfluentwidgets** - Modern Qt Theming Framework
- **Transformers** - Model loading and inference
- **Ultralytics / YOLOv9** – Region and line segmentation
- **PyMuPDF (fitz)** – PDF rasterization
- **OpenCV / scikit-image / Pillow** – Image preprocessing
- **python-docx / Qt PDF** – Export to DOCX and PDF
- **SQLAlchemy / SQLite** - Job Database
- **Nuitka** – Compilation to native standalone executable

## Recognition Pipeline

<figure style="margin-bottom: 0;">
  <img src="/resources/screens/pipeline-arch.png" alt="Pipeline architecture diagram" style="border: 1px solid #ccc;">
  <figcaption style="text-align: center; font-style: italic; color: #666; margin-top: 0.5em; margin-bottom: 0;">Textum OCR/HTR processing pipeline architecture</figcaption>
</figure>

## Internal Data Representation

- Jobs and their statuses are saved in an SQLite database.
- Each job's content is saved as a JSON file in the working directory, including the recognized text with bounding boxes.
- Both the handwritten and printed pipeline produce the same JSON format, to make post-processing easier.
- The processed images are also saved in the working directory.

### Job JSON Representation
```json
[
  {
    "page_id": "x" | "x.1" | "x.2",
    "text": ["line 1", "line 2", ...],
    "with_regions": [
      {"text": "line 1", "bbox": [x0, y0, x1, y1]},
      {"text": "line 2", "bbox": [x0, y0, x1, y1]},
      ...
    ],
    "image_path": "<working dir>/processed_images/<job_i>/PAGE1.jpg",
    "error": null | "error string"
  },
  ...
]
```
