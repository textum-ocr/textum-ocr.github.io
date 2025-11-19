# Project Structure

Overview of Textum's code organization.

### app/controller/
- `job.py` - Job execution and worker threads
- `export.py` - Export functionality

### app/models/
- `job_db.py` - SQLAlchemy job database
- `settings.py` - Application settings

### app/modules/
- `kosmos.py` - Kosmos-2.5 printed text recognition
- `trocr.py` - TrOCR handwriting recognition
- `yolo_segmentation.py` - Line/region detection for handwritten
- `preprocessing.py` - Image enhancement and image operations
- `postprocessing.py` - Spell checking, bounding box cleanup

### app/views/
- `home_view.py` - Home and Job creation interface
- `job_control_view.py` - Job management
- `review.py` - Review interface
- `settings_view.py` - Settings UI
- `export_dialog.py` - Export dialog
- `preview_widget.py` - Preview widget for job creation dialog

### resources/
- `models/` - Pretrained model weights
  - `kosmos-2.5/` - Printed text recognition model
  - `trocr/` - Handwriting recognition model
  - `yolo/` - Line and region segmentation models for handwritten
- `words/` - Spell check wordlist pickles (DE, EN, NL)
- `branding/` - Application icons and splash screen
- `sfx/` - Notification sound effects

### scripts/
Development and debugging utilities:
- `block-imports.py` - Runs Python scripts with blocked module imports for dependency testing (used to evaluate which Nuitka Python module excludes work)
- `blocklist.conf` - Configuration file for module import blocklist
- `debug_htr.py` - Debug full HTR pipeline with visualization and detailed logging
- `seed_jobs.py` - Populates database with test jobs for UI dev
- `test_stroke_enhancement.py` - Tests stroke enhancement preprocessing
- `txt2pickle.py` - Converts text wordlists to pickle format for bundling in the application
