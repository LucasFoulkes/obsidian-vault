# eSpeak NG: Setup and Usage on Windows

eSpeak NG is a lightweight, open-source speech synthesizer that supports multiple languages. It can be used directly from the command line or integrated into scripts and applications. This guide will walk you through the installation process and basic usage of eSpeak NG on Windows.

## Table of Contents

- [[#Installation|Installation]]
- [[#Adding eSpeak NG to PATH|Adding eSpeak NG to PATH]]
- [[#Using eSpeak NG in Terminal|Using eSpeak NG in Terminal]]
  - [[#Basic Command|Basic Command]]
  - [[#Adjusting Speed|Adjusting Speed]]
  - [[#Changing Voice|Changing Voice]]
  - [[#Modifying Pitch|Modifying Pitch]]
- [[#Integrating with Obsidian|Integrating with Obsidian]]
- [[#Troubleshooting|Troubleshooting]]
- [[#Additional Resources|Additional Resources]]

---

## Installation

1. Visit the [[eSpeak NG official website|http://espeak.sourceforge.net/]] and download the latest Windows version.

2. Run the installer and follow the on-screen instructions to complete the installation.

---

## Adding eSpeak NG to PATH

To use eSpeak NG from the command line, you need to add its installation directory to your system's PATH variable.

1. **Locate the installation directory:**

Find the folder where `espeak-ng.exe` is installed (e.g., `C:\Program Files\eSpeak NG`).

2. **Add to PATH:**

- Press `Win + R`, type "sysdm.cpl", and press Enter to open the System Properties window.
- Navigate to the "Advanced" tab and click on the "Environment Variables" button.
- In the "System variables" section, find the `Path` variable and click "Edit".
- Click "New" and add the full path to the eSpeak NG installation directory.
- Click "OK" to close all windows.

3. **Verify the installation:**

Open a new Command Prompt and type `espeak-ng --version`. If eSpeak NG is correctly installed and added to PATH, you should see the version information.

---

## Using eSpeak NG in Terminal

### Basic Command

```sh
espeak-ng "Hello, World!"
```

This command will make eSpeak NG say "Hello, World!" using the default settings.

### Adjusting Speed

```sh
espeak-ng -s 150 "I'm speaking faster now."
```

The `-s` option followed by a number adjusts the speaking speed. Higher values result in faster speech.

### Changing Voice

```sh
espeak-ng -v en-us+f3 "I have a different voice now."
```

The `-v` option allows you to change the voice. In this example, `en-us+f3` selects a female US English voice.

### Modifying Pitch

```sh
espeak-ng -p 75 "My pitch is higher now."
```

The `-p` option followed by a number adjusts the pitch. Higher values result in a higher pitch.

---

## Integrating with Obsidian

You can use eSpeak NG to create audio notes or to listen to your Obsidian notes:

1. Install the [[Obsidian Shell Commands|https://github.com/Taitava/obsidian-shellcommands]] plugin.

2. Configure a shell command to run eSpeak NG with the desired options, for example:

```json
{
  "platform": "Windows",
  "shell": "cmd.exe",
  "alias": "eSpeak",
  "arguments": [
    "/C",
    "espeak-ng -f \"{{file_path}}\" -w \"{{file_path}}.wav\""
  ]
}
```

3. Run the shell command on the current note to generate an audio file.

You can also use the [[Obsidian Audio Recorder|https://github.com/elias-sundqvist/obsidian-audio-recorder]] plugin to record and embed audio notes in your vault.

---

## Troubleshooting

If you encounter issues with eSpeak NG, check the following:

- Ensure that eSpeak NG is installed correctly and the installation directory contains the `espeak-ng.exe` file.
- Verify that the eSpeak NG installation directory is added to the system's PATH variable.
- Restart your terminal or Command Prompt after making changes to the PATH variable.

If the issue persists, consult the [[official eSpeak NG documentation|http://espeak.sourceforge.net/docindex.html]] for further assistance.

---

## Additional Resources

- [[eSpeak NG Official Website|http://espeak.sourceforge.net/]]
- [[eSpeak NG GitHub Repository|https://github.com/espeak-ng/espeak-ng]]
- [[eSpeak NG Documentation|http://espeak.sourceforge.net/docindex.html]]
- [[Obsidian Shell Commands Plugin|https://github.com/Taitava/obsidian-shellcommands]]
- [[Obsidian Audio Recorder Plugin|https://github.com/elias-sundqvist/obsidian-audio-recorder]]

#eSpeak #Windows #TextToSpeech #OpenSource #SpeechSynthesis #Obsidian #Plugins
