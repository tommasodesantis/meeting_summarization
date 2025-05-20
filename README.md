# Google Colab Script: Transcribe Audio & Generate Summaries - A Low-Cost Alternative

This script is designed as a low-cost alternative to expensive transcription and summarization services like Otter.ai, putting powerful AI tools in your hands.

This Google Colab script automates the process of transcribing audio files (MP3s) and generating concise summaries of the transcribed text. It leverages **AssemblyAI** for accurate speech-to-text transcription and **OpenRouter** (e.g., with Google's Gemini Flash) for intelligent summarization. A key feature is its integration with **Google Drive**, enabling streamlined workflows—especially when used with Google Drive Desktop.

---

## Overview

The script provides two main functionalities:

- **Transcribe and Summarize**: Upload or select an MP3 audio file from your Google Drive, transcribe it, and then generate a summary.
- **Summarize Existing Transcript**: Select an existing `.txt` transcript file from your Google Drive and generate a summary.

Both transcripts and summaries are saved back to your specified Google Drive folder.

---

## Features

- **Accurate Transcription**: Uses AssemblyAI’s universal speech model with automatic language detection and speaker labeling.
- **Intelligent Summarization**: Employs an LLM via OpenRouter (e.g., `google/gemini-2.5-flash-preview`) to produce summaries that highlight key points, decisions, and action items.
- **Google Drive Integration**: Reads from and writes to a user-defined Google Drive folder.
- **User-Friendly Interface**: Provides guided prompts and menus in the Colab environment.
- **Flexible Recording Options**: Record audio using any preferred tool (e.g., **Audacity**, **Voicemeeter**).
- **Automation Potential**: Optimized for workflows using **Google Drive Desktop**.

---

## Requirements

- A Google Account (for Google Colab and Google Drive).
- **API Keys**:
  - **AssemblyAI API Key**: For transcription.
  - **OpenRouter API Key**: For summarization (or any OpenAI-compatible key).
- **Python Libraries**: `assemblyai`, `openai`, `google-colab` (installed by the first cell).

---

## Setup Instructions

1. **Open the Notebook in Google Colab.**

2. **Install Libraries**  
   Run the first cell: `# @title 0. Install Libraries`

3. **Configure API Keys**  
   In the Colab interface:
   - Click the 🔑 **Secrets** icon in the left sidebar.
   - Add secrets:
     - Name: `ASSEMBLYAI_API_KEY`, Value: _your key_
     - Name: `OPENROUTER_API_KEY`, Value: _your key_

4. **Configure Google Drive Path**  
   In the second cell: `# @title 1. Setup, Configuration, and User Intent`
   - Set the `DRIVE_BASE_FOLDER_PATH` variable to your desired folder, e.g.,  
     `'MyDrive/MyMeetingRecordings'` or `'MyDrive/ProjectX/AudioLogs'`.

---

## How to Use

### 1. Recording Your Meetings

- Use tools like **Zoom**, **OBS**, or **Audacity** to record.
- Ensure the file is saved as **MP3**.
- Place the MP3 file into the folder set by `DRIVE_BASE_FOLDER_PATH`.

### 2. Running the Notebook

- **Run Installation Cell**  
  `# @title 0. Install Libraries`

- **Run Setup & Intent Cell**  
  `# @title 1. Setup, Configuration, and User Intent`  
  You'll be prompted to choose an option:
  - `1`: Transcribe a new audio file and summarize it.
  - `2`: Summarize an existing `.txt` transcript.

- **Run Main Logic Cell**  
  `# @title 2. Main Script Logic: Processing and Summarization`  
  - Authorize Google Drive access.
  - Select the MP3 or transcript file by number.
  - The script will transcribe (if needed) and summarize.
  - Output files are saved to your Google Drive folder with informative filenames.

---

## Automation with Google Drive Desktop

**Use case**: Streamline recording-to-summary workflows.

1. **Install Google Drive Desktop** and sync a local folder.

2. **Update `DRIVE_BASE_FOLDER_PATH`** in the script to match the synced Drive folder (e.g., `'MyDrive/MySyncedMeetings'`).

3. **Workflow**:
   - Save your MP3 into the synced folder.
   - Drive syncs it automatically.
   - Launch the Colab script and select the file—no manual uploads needed.

---

## Customization

- **Summarization Model**  
  Modify the model used in `openrouter_client.chat.completions.create()`.  
  Ensure it’s supported by your OpenRouter or equivalent provider.

- **System Prompt**  
  Edit the system prompt to adjust tone, style, or detail level.

- **Transcription Configuration**  
  Update `aai.TranscriptionConfig` for advanced settings like:
  ```python
  speech_model=aai.SpeechModel.universal
  language_detection=True
---

## Troubleshooting & Notes

- Ensure your API keys are correctly added to Colab secrets and have notebook access enabled.
- Double-check the `DRIVE_BASE_FOLDER_PATH` is accurately set to an existing or creatable path in your Google Drive.
- If transcription or summarization fails, check the error messages printed by the script. This often relates to:
  - API key issues
  - Model availability
  - Problems with the input file
- For very long audio files, transcription and summarization can take a significant amount of time and may hit:
  - API rate limits
  - Token limits for summarization

---

This script aims to provide a powerful yet easy-to-use tool for managing and understanding your audio recordings. **Enjoy the automation!**
