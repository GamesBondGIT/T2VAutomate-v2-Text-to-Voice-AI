# T2V Desktop Suite (Windows)

This document outlines the architecture, functionalities, and user interface for the **T2V Desktop Application** (	2vautomatedesktop), a native PySide6/Qt desktop app designed to process text-to-voice generation powerfully and efficiently on Windows.

## 1. Core Functionality & Storage Architecture

The desktop app interacts natively with the Windows file system, ensuring easy access to deliverables and global configurations.

- **Root Directory**: C:\Users\hi\Documents\T2Vautomate
  - Used as the primary workspace for all desktop processing.
- **Output Folders (ddMMyy)**: Generated audio files are stored in date-stamped folders (e.g., 220926). Inside each folder, the app saves:
  1. [ScriptName]_ref.txt (The AI-refined script)
  2. [ScriptName]_vm.txt (The character-to-voice mapping applied, formatted as Charname : assigned voice name (ID) (LANguageCode))
  3. [ScriptName]_ad.mp3 (The final synthesized audio file)
- **Temporary Data**: A hidden .temp folder inside the root handles intermediate chunk downloads and concatenations.
- **Global Config**: global_voice_map.json is stored at the root, allowing cross-session memory of character-to-voice pairings.
- **Auto-Open**: Upon successful completion of either a Manual or Auto mode job, Windows File Explorer automatically opens the output directory.

## 2. User Interface (UI)

The UI is built with **PySide6 (Qt for Python)**, styled with a premium dark mode, pink/orange accent colors, and custom CSS for sleek native desktop widgets. The application is strictly locked to a minimum 16:9 aspect ratio (1280x720) to prevent UI distortion while allowing for fullscreen scaling.

### A. Main Window Layout
The main entry point provides a fixed sidebar navigation structure:
- **T2V Automate (Batch Processing)**: Selected via the "Auto Mode" sidebar button (Pink Accent).
- **T2V Manual (Controlled Processing)**: Selected via the "Manual Mode" sidebar button (Orange Accent).
- **Settings**: Global app configuration selected via the "Settings" sidebar button (Blue Accent).

### B. T2V Automate (Pink Theme)
Designed for one-click batch processing of multiple scripts, bypassing the need for manual character mapping.
- **Queue Widget**:
  - Displays a scrollable native list of queued .txt scripts.
  - Buttons: "Add Scripts", "Output Folder", and a large "GENERATE AUDIO" action button.
  - **Dynamic Queue Logic**: Queue items hold absolute file paths securely in memory. Scripts can be added in bulk, and removed using individual "X" buttons. The X button is hidden during active generation.
- **Generation Settings**:
  - GPT Model (Combobox, Default: **GPT-5.1**)
  - Refinement Pack (Combobox, Default: **Natural American KidFriendly Pack Long**)
  - TTS Model (Combobox, Default: **Eleven v3**)
  - Stability (Combobox, Default: **Creative (0.0)**)
  - Speed Slider (
