# Building from Source

Build Textum into a standalone executable using Nuitka. Includes Python runtime, CUDA 12.8 runtime, dependencies, and application code.

**Build Time**: Several hours due to complex dependencies (torch, transformers). Nuitka compiles Python to C then to native machine code.

**Note**: Installing ccache can help with build time (Nuitka should install ccache automatically on Windows. On Linux, use your package manager)

## Prerequisites

**Linux**:
- Python 3.13
- GCC compiler
- 16GB+ RAM
- ~20GB disk space

**Windows**:
- Python 3.12.10
- 16GB+ RAM (more than 16GB strongly recommended - past builds have failed with 16GB)
- ~20GB disk space

## Models

Before building, you need to download the required machine learning models (~7GB total). See [Machine Learning Models](model.md) for download instructions.

## Linux Build

```bash
# setup
python -m venv .venv-linux
source .venv-linux/bin/activate
pip install -r requirements.txt

# download models (see Models section above)

# recommeded: install ccache
sudo apt install ccache

# build
bash build.sh

# verify
./dist/textum.dist/textum
```

### What build.sh does:
- Uses Nuitka to compile Python to standalone executable
- Requires torch_shm_manager binary from torch package
- Excludes unused transformers models via `--nofollow-import-to` flags
- Generates `dist/textum.dist/` folder with executable and dependencies
- Creates `dist/textum-dist-linux.tar.gz` archive

## Windows Build

### Install Python 3.12.10

```powershell
Invoke-WebRequest -Uri "https://www.python.org/ftp/python/3.12.10/python-3.12.10-amd64.exe" -OutFile "python-installer.exe"
# this command may conflict with existing python installations
Start-Process -FilePath .\python-installer.exe -ArgumentList "/quiet InstallAllUsers=1 PrependPath=1" -NoNewWindow -Wait
```

### Install Microsoft C++ Runtime

```powershell
Invoke-WebRequest "https://aka.ms/vs/16/release/vc_redist.x64.exe" -OutFile "vc_redist.x64.exe"
Start-Process .\vc_redist.x64.exe "/install /quiet /norestart" -Wait
```
If building still fails, try installing the `C/C++` development module from Visual Studio.

### Setup and Build

```powershell
# setup venv and install dependencies
.\build_and_run.ps1 -Install

# download models (see Models section above)

# build executable
.\build_and_run.ps1 -Build

# verify
.\dist\textum.dist\textum.exe
```

### What the build does:
- Uses Nuitka with mingw64 compiler (gcc for windows)
- Prompts for version confirmation before build
- Generates `dist/textum.dist/` folder
- Creates versioned zip archive: `dist/textum-dist-windows-<VERSION>.zip`

## Build Scripts

- `build.sh` - Linux build script using Nuitka with gcc
- `build_and_run.ps1` - Windows all-in-one script for install/build/run operations

### Customization

You can modify the build scripts to change:
- Output location
- Archive format
- Module exclusions (via `--nofollow-import-to` flags)
- Nuitka optimization flags

## Development Workflow

1. Make code changes
2. Test in dev mode:
   - Linux: `python textum.py`
   - Windows: `.\build_and_run.ps1 -Run`
3. Build executable
4. Test executable from `dist/textum.dist/`
5. Distribute if working

## Troubleshooting

### Build Fails
- Ensure 16GB+ RAM (builds have failed with less)
- Check disk space (~20GB needed)
- Verify compiler available (GCC on Linux, mingw64 via Nuitka on Windows)
- Review build logs for specific errors
- Try clean build: remove `dist/` folder and rebuild

### "No Space Left on Device" (Linux)
- Check tmpfs usage: `df -h /tmp`
- Nuitka makes extensive use of `/tmp` during compilation
- Increase tmpfs capacity or clean up temporary files

### Windows Defender Issues
- Add build directory to Windows Defender exclusions
- Temporarily disable real-time scanning during build
- Check temp directory permissions
- If errors persist, check Windows Defender quarantine logs

### Scons Backend Compilation Failed
- This usually occurs on Windows
- System memory may not be sufficient (usually needs 16GB+)
- Windows Defender may have deleted intermediate build files during automated scan
- Check `...\AppData\Local\Temp\1` for missing files
- Solution: Add temp directory to exclusions and rebuild

### Long Build Times
- Normal behavior - can take several hours
- Use ccache for faster rebuilds (should auto-install on Windows)
- Linux: `sudo apt install ccache`
- Subsequent builds will be faster

## Distribution

Models are bundled in the build. The `resources/models/` directory is included with the executable.

**For distribution**:
- Package the entire `dist/textum.dist/` folder as an archive
- Linux: tar.gz format
- Windows: zip format

**For users**:
- Extract the archive
- Run the executable **from the extracted folder**

## Note on uv

Use standard `python -m venv` instead of uv. Nuitka works best with standard virtual environments (there were some issues with nuitka + uv in the past).
