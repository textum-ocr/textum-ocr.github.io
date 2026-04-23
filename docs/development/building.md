# Building from Source

Build Textum into a standalone executable using [Nuitka](https://nuitka.net). Includes Python runtime, CUDA 12.8 runtime, dependencies, and application code.

**Build Time**: Several hours due to complex dependencies (torch, transformers). Nuitka compiles Python to C then to native machine code.

**Note**: Installing [ccache](https://ccache.dev/) can help with build time (Nuitka should install ccache automatically on Windows. On Linux, use your package manager)

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

The model weights are included in the git lfs repo, no separate download is necessary.

## Linux: Running in Dev env and Building

```bash
# --- setup ---
# in the past we had problems with uv and nuitka, that's why we are using vanilla venvs
python -m venv .venv-linux
source .venv-linux/bin/activate
pip install -r requirements.txt

# --- running the app in dev env ---
python textum.py 

# --- building ---
# recommended: install ccache (example for ubuntu)
sudo apt install ccache

# build
bash build.sh

# run the binary
./dist/textum.dist/textum
```

### What build.sh does:

- Uses Nuitka to compile Python to standalone executable
- Ensures `torch_shm_manager` binary from torch package is included in final binary (past build issues)
- Excludes unused python modules via `--nofollow-import-to` flags
- Generates `dist/textum.dist/` folder with executable and dependencies
- Creates `dist/textum-dist-linux.tar.gz` archive

## Windows: Running in Dev env and Building

### Install Python 3.12.10

Python 3.13 had some issues on Windows and 3.14 is not tested at all. Stay on the 3.12.x branch for now.

Via powershell:

```powershell
Invoke-WebRequest -Uri "https://www.python.org/ftp/python/3.12.10/python-3.12.10-amd64.exe" -OutFile "python-installer.exe"
# this command may conflict with existing python installations!
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

# run textum from the dev environment
.\build_and_run.ps1 -Run

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

## Troubleshooting

### Build Fails

- Ensure 16GB+ RAM (Windows builds have failed with less)
- Check disk space (~20GB needed)
- Verify compiler available (GCC on Linux, mingw64 via Nuitka on Windows)
- Review build logs for specific errors
- Try clean build: remove `dist/` folder and rebuild
- Check nuitka's github issues page

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
- Check `...\AppData\Local\Temp\1` for missing files (Scons stores intermediate assembly files here and Windows Defender doesn't like that)
- Possible Solution: Add that temp directory to exclusions and rebuild

### Long Build Times

- Normal behavior - can take several hours
- Use ccache for faster rebuilds (Windows: should auto-install, Linux: use your package manager)
- Subsequent builds should be faster

## Distribution

Models are bundled in the build. The `resources/models/` directory is included with the executable.

**For distribution**:

- Package the entire `dist/textum.dist/` folder as an archive. This is automatically done by both build scripts.
- Linux: tar.gz format
- Windows: zip format

**For users**:

- Extract the archive
- Run the executable **from the extracted folder**
