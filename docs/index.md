---
hide:
  - navigation
---

# **Textum**

<figure style="text-align: center; margin-bottom: 0;">
  <img src="/resources/screens/review-header.png" alt="Textum Review interface preview" style="border: 1px solid #ccc;">
  <figcaption style="text-align: center; font-style: italic; color: #666; margin-top: 0.5em; margin-bottom: 0;">Textum Review interface preview</figcaption>
</figure>

Textum is a desktop application for handwritten and printed text recognition. It contains a sophisticated review interface and handles all steps of the workflow: from input files, to text recognition, manual review and exporting to various formats. Textum works fully offline and doesn't send any data to external services. The application is provided free of charge.

🛠️ The Source Code can be found here: [codeberg.org/textum/app](https://codeberg.org/textum/app).

🖼️ If you want to see more of the interface, visit the [Gallery](getting-started/gallery.md).

## Features

- Easy installation. Just download, extract and start working
- Process single images, PDFs, or folders of images
- Printed text recognition with [Kosmos-2.5](https://huggingface.co/microsoft/kosmos-2.5)
- Handwritten text recognition with [TrOCR](https://huggingface.co/microsoft/trocr-base-handwritten) (fine-tuned on holocaust diaries)
- Models are bundled with the application, no separate downloads needed
- Intuitive side-by-side review interface
- Automated highlighting of likely OCR errors, via dictionaries (currently German, English, Dutch)
- Export to plain text, DOCX, or PDF. ALTO or PAGE XML are currently not yet supported
- Works fully offline. No data is sent anywhere.

## ▶️ Next Steps

- 😀 Users: proceed to the [Installation](getting-started/installation.md)
- 🛠️ Developers: See how to [build and run the app locally](development/building.md)

## System Requirements

- CUDA-capable GPU (recommended, but not required)
- 8GB RAM should work, but 16GB is better
- ~20GB disk space
- Windows 10/11 or Linux. MacOS is not tested

## How It Works

1. **Preprocess** - Image enhancement and normalization
2. **Segment** - YOLO-based line and region detection (handwritten only)
3. **Recognize** - Kosmos-2.5 (printed) or TrOCR (handwritten)
4. **Postprocess** - Spell checking and corrections
5. **Review** - Manual verification and editing
6. **Export** - Save as text, DOCX, or PDF

