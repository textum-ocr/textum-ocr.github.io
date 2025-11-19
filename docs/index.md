# Textum

Textum is a desktop application for handwritten and printed text recognition. It contains a sophisticated review interface and handles all steps of the workflow: from input files, to text recognition, manual review and, finally, exporting to various formats. Textum works fully offline and doesn't send any data to external services. The application is provided free of charge.

## Features

- Process single images, PDFs, or folders of images
- Printed text recognition with Kosmos-2.5
- Handwritten text recognition with TrOCR (fine-tuned on historical documents)
- Multi-language spell checking (German, English, Dutch)
- Interactive side-by-side review interface
- Export to plain text, DOCX, or PDF
- Models bundled with application (no separate downloads needed)

## Quick Links

- [Quick Start](getting-started/quick-start.md) - Create your first job
- [User Guide](user-guide/overview.md) - Complete usage guide
- [Building from Source](development/building.md) - For developers

## System Requirements

- CUDA-capable GPU (strongly recommended)
- 8GB RAM minimum, 16GB recommended
- ~20GB disk space
- Windows 10/11 or Linux

## How It Works

1. **Preprocess** - Image enhancement and normalization
2. **Segment** - YOLO-based line and region detection (handwritten only)
3. **Recognize** - Kosmos-2.5 (printed) or TrOCR (handwritten)
4. **Postprocess** - Spell checking and corrections
5. **Review** - Manual verification and editing
6. **Export** - Save as text, DOCX, or PDF

