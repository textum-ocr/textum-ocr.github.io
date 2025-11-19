# Troubleshooting

Common issues and possible solutions.

## Installation Issues

### Models Not Detected
**For users**: Models should be bundled with the application. If missing, re-download the application.

**For developers**:
- Verify models in `resources/models/`
- Check directory structure matches expected layout
- Ensure all files present (not just directories)
- Check file permissions
- Review application log

### CUDA Issues
- Verify GPU is available
- Windows: ensure drivers are installed and up-to-date
- Check CUDA version compatibility (12.8 is supported)
- Check GPU memory availability

## Runtime Issues

### Application Won't Start
- Check application log
- Run from command line for errors
- Check system requirements (RAM, disk)

### Slow Application start
- If you're hardware is older you may experience a long application start

### Jobs Fail to Start
- Check input files exist and accessible
- Verify file permissions
- Check disk space
- Ensure models loaded
- Check GPU memory
- Review application log

### Recognition Errors
- Check image quality (resolution, contrast)
- Verify correct job type (printed vs handwritten)
- Ensure correct language selected
- Try preprocessing images
- Check model files complete
- However, it may just be that the recognition methods currently implemented in Textum are not fit for your specific document style

### Out of Memory
- Reduce max concurrent jobs (Settings)
- Process smaller batches
- Close other applications
- Check available RAM/VRAM
- Process images individually

## User Interface Issues

### Interface Not Responding
- Running a job may be resource hungry and slow the entire system down
- Reduce concurrent jobs
- Check system resources
- Restart application
- Review log

## Performance Issues

### Slow Processing
- Check GPU being used (not CPU)
- Verify CUDA working
- Reduce image resolution if very large
- Process fewer pages at once
- Ensure models loaded (not reloading)
- Check system resources

### High Memory Usage
- Reduce concurrent jobs
- Process smaller batches
- Close other applications
- Restart app periodically
- Monitor memory usage

## Export Issues

### Export Fails
- Check disk space
- Verify write permissions
- Ensure job completed
- Check file path length
- Try different format
- Review log

## Application Logs

**Location**: Working directory/log.txt

Check logs for:
- Error messages
- Timestamps
- Specific error codes
- Stack traces

## System Information for Reporting

When reporting issues, include:
- OS and version
- Python version
- GPU model and drivers
- Textum version
- Error messages from logs
- Steps to reproduce

## Quick Fixes

- **Restart Application** - Fixes many temporary issues
- **Check Logs** - Provides specific error details
- **Verify Models** - Ensure all present and correct
- **Check Resources** - RAM, disk space, GPU memory
- **Update Dependencies** - Ensure latest versions
- **Clean Install** - Remove and reinstall if needed
