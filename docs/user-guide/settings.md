# Settings

Configure Textum through the Settings view.

<figure style="margin-bottom: 0;">
  <img src="/resources/screens/settings.png" alt="Settings View" style="border: 1px solid #ccc;">
  <figcaption style="text-align: center; font-style: italic; color: #666; margin-top: 0.5em; margin-bottom: 0;">Settings view for configuring application preferences</figcaption>
</figure>

## General

### Auto-Start Jobs
Automatically start pending jobs when the application launches.
**Use for**: Batch processing workflows

### Notification Sound
Play a sound when jobs complete.
**Use for**: Background processing

### Max Concurrent Jobs
Maximum jobs to process simultaneously.
**Default**: 3
**Note**: Higher values use more resources and may slow down your PC

## Advanced

### Working Directory
Directory for job data, outputs, and logs. Usually you don't need to change this.
**Default**: System-specific location
**Change**: Browse to select new location

Default locations are:

- **Linux**: `~/.cache/textum-data/`
- **Windows**: `%LOCALAPPDATA%/textum-data/`

### Application Log
Opens the application log.
**Location**: `<working_directory>/log.txt`

### Reset Review Help Dialog
If you selected `Don't show this again` in the explanatory pop-up when opening the review view, this option resets that preference.
