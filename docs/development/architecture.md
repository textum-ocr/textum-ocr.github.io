# Architecture

System design and architecture overview.

## Technology Stack

- **PySide6** - Cross-platform GUI
- **Transformers** - Model loading and inference
- **PyTorch** - Deep learning backend
- **SQLAlchemy** - Database persistence
- **Nuitka** - Python to executable compilation

## Application Flow

1. **Startup** - Load settings, configure logging, initialize database
2. **Model Loading** - On-demand with GPU memory management
3. **UI** - Main window with views, event handling
4. **Event Loop** - User interactions, job processing, UI updates

## Job Processing

```
User Input → Job Creation → Database → Worker Thread
                                            ↓
                                      Preprocessing
                                            ↓
                                       Recognition
                                            ↓
                                     Postprocessing
                                            ↓
                                    Results Storage
                                            ↓
                                   Review Interface
                                            ↓
                                         Export
```

## Components

### Controllers
- **JobController** - Manages job lifecycle, worker threads, status, concurrency
- **ExportController** - Format conversion, file generation

### Models
- **JobDB** - SQLAlchemy persistence, status tracking
- **Settings** - Configuration storage, user preferences

### Recognition Modules
- **Kosmos** - Printed text recognition, layout understanding
- **TrOCR** - Handwritten text recognition
- **YOLO** - Region and line segmentation (for handwritten)
- **Preprocessing** - Image enhancement
- **Postprocessing** - Spell checking, corrections

### Views
- **HomeView** - Job creation
- **JobControlView** - Job management
- **ReviewView** - Text editing
- **SettingsView** - Configuration

## Concurrency

**Threads**:
- Main - UI and event loop
- Workers - Job processing (one per job)
- Model - Handled by PyTorch

**Synchronization**: SQLAlchemy for database, Qt signals/slots for UI, thread-safe model loading

## Memory Management

- Models loaded on-demand, cached, cleaned up on exit
- Job data in database, loaded as needed
- GPU memory carefully managed

## Error Handling

- Errors caught in workers, status updated, user notified, logs recorded
- Graceful degradation for model errors

