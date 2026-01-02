# AI Reel Generator

A Flask-based web application that automatically generates Instagram Reels/short videos by stitching together uploaded images/videos and adding AI-generated voiceovers using ElevenLabs.

## Features

- **Web Interface**: Simple and clean UI to upload media and enter script text.
- **AI Voiceover**: Uses [ElevenLabs API](https://elevenlabs.io/) to convert text to realistic speech.
- **Automatic Editing**: Stitches uploaded media with the generated audio using FFmpeg.
- **Background Processing**: Handles video generation in the background to keep the UI responsive.
- **Gallery**: View generated reels directly from the browser.

## Prerequisites

Before running the application, ensure you have the following installed:

1.  **Python 3.8+**
2.  **FFmpeg**: This is critical for video processing.
    -   *Windows*: Download from [gyan.dev](https://www.gyan.dev/ffmpeg/builds/) and add `bin` to your System PATH.
    -   *Mac*: `brew install ffmpeg`
    -   *Linux*: `sudo apt install ffmpeg`

## Installation

1.  **Clone the repository** (if applicable) or navigate to the project directory.

2.  **Install Python dependencies**:
    ```bash
    pip install -r requirements.txt
    ```

3.  **Environment Setup**:
    Create a `.env` file in the root directory (or ensure the existing one is configured). It must contain your ElevenLabs API key:
    ```env
    ELEVENLABS_API_KEY=your_api_key_here
    ```

## Usage

1.  **Start the Application**:
    Run the main Flask server:
    ```bash
    python main.py
    ```

2.  **Start the Background Processor**:
    Open a *separate* terminal window and run the processor script. This daemon listens for new uploads and processes them.
    ```bash
    python generate_process.py
    ```

3.  **Create a Reel**:
    -   Open your browser and go to `http://127.0.0.1:5000`.
    -   Click "Start Creating Now".
    -   Upload images or video clips.
    -   Enter the text you want the AI to read.
    -   Click "Create Reel".

4.  **View Results**:
    -   Once processed, results will appear in the "Gallery" section or can be found in `static/reels`.

## Project Structure

```
├── main.py                 # Main Flask application entry point
├── generate_process.py     # Background script for audio/video processing
├── text_to_audio.py        # Wrapper for ElevenLabs text-to-speech API
├── templates/              # HTML templates (Jinja2)
├── static/                 # CSS, images, and generated reels
├── user_uploads/           # Temporary storage for user uploads
└── done.txt                # Log file tracking processed folders
```

## Troubleshooting

-   **FFmpeg not found**: Ensure `ffmpeg` is accessible from your terminal. Run `ffmpeg -version` to verify.
-   **Audio not generating**: Check your ElevenLabs API key in `.env` and quota limits.
-   **Permission errors**: Ensure the script has write permissions to `user_uploads` and `static/reels` folders.
