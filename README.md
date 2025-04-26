# Derupt - Voice-to-Obsidian Capture App

A zero-friction voice note capture tool that transcribes your voice notes and saves them directly to your Obsidian vault.

## Features

- Global hotkey trigger for instant voice capture
- Voice-activated stop (automatic silence detection)
- OpenAI Whisper API transcription
- Automatic save to Obsidian Vault as markdown
- Daily Note linking
- Background system tray operation
- User notifications for successful and failed operations

## Requirements

- Node.js and npm
- Obsidian installed with a vault created
- OpenAI API key

## Configuration

The app uses a config file located at:

- Windows: `%APPDATA%\Derupt.ai\config.json`
- macOS: `~/Library/Application Support/Derupt.ai/config.json`
- Linux: `~/.config/Derupt.ai/config.json`

### Configuration Options

```json
{
  "obsidianPath": "",        // Path to your Obsidian app folder
  "vaultName": "",           // Name of your Obsidian vault
  "noteDir": "VoiceNotes",   // Path within your Obsidian vault where voice notes will be saved

  "dailyNote": {
    "enabled": false,        // Whether to link to daily notes
    "dateFormat": "YYYY-MM-DD", // Date format for daily notes
    "newFileLocation": "Daily", // Directory for daily notes
    "templateFileLocation": "Daily/Template" // Template file path
  },

  "silenceThreshold": 60.0,      // RMS threshold for silence detection
  "maxSilenceDuration": 3000,    // Max silence duration in ms before stopping
  "hotkey": "CommandOrControl+Shift+V", // Global hotkey for voice capture

  "transcribeApiKey": "",        // Your OpenAI/Whisper API key
  "transcribeModel": "whisper-1",
  "transcribeUri": "https://api.openai.com/v1/audio/transcriptions"
}
```

### OpenAI API Key

The app requires an OpenAI API key to use the Whisper API for transcription. If the key is missing:

1. A notification will appear when the app starts
2. Clicking the notification will open the configuration directory
3. Edit the `config.json` file to add your API key
4. Save the file and restart the app

You can also access the configuration directory from the tray menu.

## Usage

1. Run the app (it will minimize to the system tray)
2. Press the configured hotkey (default: Ctrl+Shift+V or Cmd+Shift+V on Mac) to start recording
3. Speak your note
4. Recording will automatically stop after detecting silence
5. Your transcribed note will be saved to your Obsidian vault
6. Click the notification to open the note in Obsidian

## Troubleshooting

- If you see a notification about configuration errors, click it to open the config directory and fix the issues
- If you see a notification about a missing OpenAI API key, click it to open the config directory and add your key
- If the app doesn't recognize the global hotkey, try restarting or using a different key combination
- Check the log files for detailed error messages (accessible from the tray menu via "Open Log Directory")
- The app will exit after displaying configuration error notifications; fix the issues and restart the app

## Logging

The application logs all activity to log files in the following location:

- Windows: `%APPDATA%\Derupt.ai\logs\`
- macOS: `~/Library/Application Support/Derupt.ai/logs/`
- Linux: `~/.config/Derupt.ai/logs/`

Log files are named by date (e.g., `derupt-2023-05-15.log`) and contain detailed information about application activity, errors, and warnings. You can access the log directory from the tray menu by clicking "Open Log Directory".
