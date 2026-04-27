# Argus-S.E.E

ARGUS — Local AI Agent

A fully local, voice-activated AI agent with complete PC control, built with Python and Godot 4.


What is ARGUS?
ARGUS is a personal AI assistant that runs entirely on your machine — no cloud, no subscriptions, no internet required. It listens for your wake word, understands your voice, controls your PC, remembers things about you, and responds with a robotic British voice. It has its own eye UI built in Godot 4.

Features

Wake word detection — say "Hey Argus" to activate or one of {"wake up"; "hey computer"; "wake up computer"}
Speech to text via Whisper (runs on CPU)
AI responses via Ollama (fully local, no API key needed)
Text-to-speech with GLaDOS-style robotic British voice
Complete PC control — mouse, keyboard, files, apps, terminal
Camera support (optional)
Persistent memory — stores facts and full conversation history
Email — read and send via Gmail
Web scraping and DuckDuckGo search
Battery and volume monitoring
Godot 4 animated eye UI with waveform display
Text input mode — type instead of speaking
Everything stored locally in a data/ folder


Requirements
Minimum specs

Windows 10 or 11
4GB RAM (8GB recommended)
Python 3.11 or higher
Microphone

Software

Python 3.11+
Ollama
Godot 4 (for the UI)
Vosk small English model — vosk-model-small-en-us-0.15


Installation
1. Clone the repository
bashgit clone https://github.com/alt-paradox137/argus.git
cd argus
2. Install Python packages
bashpip install faster-whisper sounddevice numpy pyttsx3 pyautogui opencv-python pillow psutil pygetwindow requests tinydb watchdog pyperclip vosk comtypes pycaw beautifulsoup4 scipy soundfile
3. Install Ollama and pull a model
Download Ollama from https://ollama.com then run:
bashollama pull llama3.2:3b

For better responses use phi3:mini. For best quality use mistral:7b (requires 8GB RAM).

4. Download the Vosk wake word model

Go to https://alphacephei.com/vosk/models
Download vosk-model-small-en-us-0.15.zip
Extract it into ARGUS/core/

Final path should be:
ARGUS/core/vosk-model-small-en-us-0.15/
5. Configure your settings
Open core/config.py and set:
pythonOLLAMA_MODEL   = "llama3.2:3b"    # or phi3:mini
CAMERA_ENABLED = False             # set True to enable camera
EMAIL_ADDRESS  = ""                # your Gmail address (optional)
EMAIL_PASSWORD = ""                # your Gmail app password (optional)
6. Run ARGUS
Open a terminal and run:
bashcd core
python main.py
Say "Hey Argus" — it will respond.

Project Structure
ARGUS/
├── core/
│   ├── main.py           — entry point
│   ├── agent.py          — AI brain
│   ├── wake_word.py      — "Hey Argus" detection
│   ├── stt.py            — speech to text
│   ├── tts.py            — text to speech
│   ├── vision.py         — camera input
│   ├── pc_control.py     — PC control tools
│   ├── memory.py         — conversation + facts database
│   ├── tools.py          — all agent tools
│   ├── text_input.py     — text mode
│   └── config.py         — configuration
├── ui/
│   └── argus_ui/         — Godot 4 project(i love godot)
├── data/
│   ├── conversations/    — full chat history
│   ├── memory/           — stored facts
│   └── files/            — files Argus creates
└── launch_argus.bat      — launch everything at once

Usage
Voice
Just say "Wake Up" followed by any command.
Text
While main.py is running, type directly in the terminal and press Enter.
Example commands
"Hey Argus, what time is it?"
"Hey Argus, open Chrome"
"Hey Argus, take a screenshot"
"Hey Argus, what's my battery?"
"Hey Argus, remember that my name is Sunso"
"Hey Argus, search the web for weather in Tunis"
"Hey Argus, read my last 5 emails"
"Hey Argus, send an email to someone@gmail.com subject Hello body Testing"
"Hey Argus, run the command ipconfig"
"Hey Argus, open my Downloads folder"

Email Setup (optional)

Go to https://myaccount.google.com
Enable 2-Step Verification
Go to Security → App Passwords → create one for Mail
Paste the 16-character password into config.py as EMAIL_PASSWORD


Godot UI (optional)

Open Godot 4
Open the project at ui/argus_ui/
Press F5 to run
The eye will react to Argus's state — idle, listening, thinking, speaking

To export as a standalone .exe:

Project → Export → Windows Desktop → Export Project


Desktop Shortcut
Double-click launch_argus.bat to start Ollama, the Python brain, and the Godot UI all at once. Right-click it and create a desktop shortcut for easy access.

Customization
WhatWhereChange AI modelconfig.py → OLLAMA_MODELChange voice speedtts.py → sapi.RateAdd new toolstools.py → TOOLS dictAdd permanent factsagent.py → get_system_prompt()Eye animationsGodot → SpriteFrames panelWake word phrasewake_word.py → WAKE_PHRASE

Recommended Models
ModelSizeNotesllama3.2:3b2GBFast, low RAM, good defaultphi3:mini2.3GBSmarter, similar speedgemma2:2b1.6GBSmallest and fastestmistral:7b4.1GBBest quality, needs 8GB RAM

Known Limitations

Temperature monitoring requires HWiNFO or Core Temp running in background
Camera vision is basic (single frame capture)
TTS voice quality depends on installed Windows voices
Wake word accuracy depends on microphone quality and background noise


License
MIT License — free to use, modify, and distribute.

Credits
Built with:

Ollama — local LLM inference
faster-whisper — speech recognition
Vosk — wake word detection
Godot 4 — UI
pyttsx3 / Windows SAPI — text to speech
pycaw — audio control
