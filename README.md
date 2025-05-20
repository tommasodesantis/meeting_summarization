# meeting_summarization
Transcribe and summarize meetings almost for free (just the costs of AssemblyAI and Openrouter API calls).

Google Colab Script: Transcribe Audio & Generate Summaries
This script, designed for Google Colab, automates the process of transcribing audio files (MP3s) and then generating concise summaries of the transcribed text. It leverages AssemblyAI for accurate speech-to-text transcription and OpenRouter (with a model like Google's Gemini Flash) for intelligent summarization. A key feature is its integration with Google Drive, allowing for streamlined workflows, especially when combined with Google Drive Desktop.

Overview
The script provides two main functionalities:

Transcribe and Summarize: Upload or select an MP3 audio file from your Google Drive, transcribe it, and then generate a summary.

Summarize Existing Transcript: Select an existing text file (.txt) containing a transcript from your Google Drive and generate a summary.

Both the generated transcripts and summaries are saved back to your specified Google Drive folder.

Features
Accurate Transcription: Utilizes AssemblyAI's universal speech model for robust transcription across diverse audio, featuring automatic language detection and speaker labeling.

Intelligent Summarization: Employs an LLM via OpenRouter (e.g., google/gemini-2.5-flash-preview) to create detailed summaries covering main discussion points, decisions, and action items.

Google Drive Integration: Seamlessly reads audio/transcript files from and saves output files to a user-defined Google Drive folder.

User-Friendly Interface: Guides users through the process with clear prompts and file selection menus within the Colab environment.

Flexible Recording Options: You can use your favorite audio recording software (e.g., Zoom, OBS, Audacity, voice memo apps) to create your MP3 meeting recordings.

Automation Potential: Designed for easy automation, particularly with Google Drive Desktop.

Requirements
A Google Account (for Google Colab and Google Drive).

API Keys:

AssemblyAI API Key: For transcription services.

OpenRouter API Key: For summarization services (or any other OpenAI-compatible API key and endpoint you wish to configure).

Python Libraries: assemblyai, openai, google-colab (installation is handled by the first cell in the notebook).

Setup Instructions
Open the Notebook in Google Colab.

Install Libraries: Run the first cell (# @title 0. Install Libraries) to install the necessary Python packages.

Configure API Keys:

In the Google Colab interface, click the key icon (🔑) in the left sidebar to open the "Secrets" tab.

Click "+ Add a new secret".

For the Name, enter ASSEMBLYAI_API_KEY. For the Value, paste your AssemblyAI API key. Toggle "Notebook access" ON.

Click "+ Add a new secret" again.

For the Name, enter OPENROUTER_API_KEY. For the Value, paste your OpenRouter API key. Toggle "Notebook access" ON.

Configure Google Drive Path:

In the second cell of the notebook (# @title 1. Setup, Configuration, and User Intent), locate the DRIVE_BASE_FOLDER_PATH variable.

Crucially, update this path to your desired folder within your Google Drive where your MP3s are (or will be) stored, and where you want transcripts and summaries to be saved. For example: 'MyDrive/MyMeetingRecordings' or 'MyDrive/ProjectX/AudioLogs'.

The script will attempt to create this folder if it doesn't exist when you run the main logic cell.

How to Use
1. Recording Your Meetings
Use any recording software you prefer to capture your meetings or audio.

Ensure the final audio is saved or converted to MP3 format.

Place these MP3 files into the Google Drive folder you configured in DRIVE_BASE_FOLDER_PATH.

2. Running the Notebook
Run the Installation Cell: Execute the first cell (# @title 0. Install Libraries) to install dependencies.

Run the Setup & Intent Cell: Execute the second cell (# @title 1. Setup, Configuration, and User Intent).

This cell imports libraries, loads your API keys from secrets, and prompts you to choose an operation:

1: Transcribe a new audio file and then summarize it.

2: Summarize an existing transcript file (.txt).

Run the Main Logic Cell: Execute the third cell (# @title 2. Main Script Logic: Processing and Summarization).

Mount Google Drive: You will be prompted to authorize Google Drive access.

File Selection:

If you chose option 1, the script will list MP3 files from your configured Drive folder. Enter the number corresponding to the file you want to process.

If you chose option 2, the script will list .txt files. Enter the number corresponding to the transcript you want to summarize.

Processing: The script will then perform the transcription (if applicable) and summarization.

Output: Generated transcripts and summaries will be saved to your specified Google Drive folder with filenames indicating the original file and date/time of processing.

Automation with Google Drive Desktop
The Google Drive integration is particularly powerful when used with the Google Drive Desktop application.

Set up Google Drive Desktop: Install and configure Google Drive Desktop on your computer to sync a local folder with your Google Drive.

Configure DRIVE_BASE_FOLDER_PATH: In the Colab script, set DRIVE_BASE_FOLDER_PATH to point to the synced folder within your Google Drive (e.g., if your local synced folder C:\Users\YourName\MySyncedMeetings appears as MyDrive/MySyncedMeetings in Google Drive, use the latter).

Automated Workflow:

Save your meeting recordings (as MP3s) directly into this local synced folder on your computer.

Google Drive Desktop will automatically upload/sync the MP3 to your Google Drive.

When you run the Colab script, the new MP3 will be available for selection without needing to manually upload it to Google Drive through the web interface or move it within Drive. This significantly streamlines the process from recording to summarization.

Customization
Summarization Model: You can change the LLM model used for summarization by modifying the model parameter in the openrouter_client.chat.completions.create() call within the script. Ensure the model is available through your OpenRouter (or other configured) API.

System Prompt: Adjust the system prompt provided to the LLM to tailor the style or focus of the summaries.

Transcription Configuration: Modify the aai.TranscriptionConfig parameters if you have specific transcription needs. The script defaults to speech_model=aai.SpeechModel.universal and language_detection=True.

Troubleshooting/Notes
Ensure your API keys are correctly added to Colab secrets and have notebook access enabled.

Double-check the DRIVE_BASE_FOLDER_PATH is accurately set to an existing or creatable path in your Google Drive.

If transcription or summarization fails, check the error messages printed by the script. This often relates to API key issues, model availability, or problems with the input file.

For very long audio files, transcription and summarization can take a significant amount of time and may hit API rate limits or token limits for summarization.

This script aims to provide a powerful yet easy-to-use tool for managing and understanding your audio recordings. Enjoy the automation!
