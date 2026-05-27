# 💪 AI Real-Time GYM Coach

> A real-time AI-powered fitness coach that tracks your exercise form through your webcam, counts reps, and delivers live voice feedback — right in your browser.
---

## 🔗 Live Demo

| | Link |
|---|---|
| 🌐 Landing Page | [realtime-gymcoach-ai.netlify.app](https://realtime-gymcoach-ai.netlify.app/) |
| 🚀 Main App | [realtime-ai-gymcoach.streamlit.app](https://realtime-ai-gymcoach.streamlit.app/) |

---
![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-1.54-FF4B4B?logo=streamlit&logoColor=white)
![MediaPipe](https://img.shields.io/badge/MediaPipe-0.10-00C7B7?logo=google&logoColor=white)
![Groq](https://img.shields.io/badge/LLM-Groq-orange)

## ✨ Features

- **Real-Time Pose Detection** — Uses MediaPipe to track body landmarks via your webcam, frame by frame
- **Rep & Set Counter** — Automatically counts reps and tracks sets against your workout plan
- **Form Analysis** — Measures joint angles and body alignment to evaluate your exercise form in real time
- **AI Voice Coaching** — Groq LLM generates contextual coaching cues; gTTS converts them to speech and plays them back instantly
- **5 Supported Exercises** — Squats, Push-ups, Bicep Curls, Shoulder Press, and Lunges
- **Exercise-Specific Metrics** — Each exercise surfaces relevant metrics (knee angle, elbow angle, back arch, balance status, etc.)
- **Workout History** — Persists your rep/set/time data per session with an aggregated history table
- **User Authentication** — Login wall to support multi-user sessions

---

## 🧠 How It Works

```
Webcam Feed
    │
    ▼
MediaPipe Pose Estimation  ──►  Joint Angle Calculation
    │                                    │
    ▼                                    ▼
Rep Counter / Set Tracker       Form Feedback Signals
    │                                    │
    └────────────────┬───────────────────┘
                     ▼
              Groq LLM Coach  ──►  gTTS Voice Output
                     │
                     ▼
           Streamlit UI (WebRTC)
```

The app streams your webcam through WebRTC into a `VideoProcessor` that runs MediaPipe on every frame. Detected landmarks feed into exercise-specific detectors that track reps and form. On key events (workout start, set complete, bad form), the `VoicePipeline` calls Groq to generate coaching text, converts it to audio via gTTS, and autoplays it in the browser.

---

## 🗂️ Project Structure

```
AI-Real-Time-GYM-Coach/
├── main.py                   # Streamlit app entry point
├── requirements.txt
├── packages.txt
├── .streamlit/               # Streamlit config
├── core/                     # Shared utilities and base classes
├── detectors/                # Exercise-specific rep & form detectors
├── ml_models/                # Pose model wrappers
├── services/
│   ├── auth/                 # Login wall
│   ├── coaching/             # LLM coach, TTS, voice pipeline
│   ├── config/               # Exercise options config
│   ├── persistence/          # SQLite workout history
│   ├── state/                # Session state defaults
│   ├── tracking/             # Metrics sync
│   ├── ui/                   # CSS / style loaders
│   └── vision/               # WebRTC video processor
└── static/                   # CSS and fonts
```

---

## ⚙️ Tech Stack

| Layer | Technology |
|---|---|
| Frontend / UI | Streamlit + WebRTC |
| Pose Estimation | MediaPipe |
| LLM Coaching | Groq (`llama` / `gemma` models) |
| Text-to-Speech | gTTS |
| Data Persistence | SQLite via Pandas |
| Landing Page | Netlify (static HTML/CSS) |
| Deployment | Streamlit Community Cloud |

---

## 🚀 Quick Start

**Prerequisites:** Python 3.11+, a webcam, and a [Groq API key](https://console.groq.com/)

```bash
# 1. Clone the repo
git clone https://github.com/yuvrajrathore672/AI-Real-Time-GYM-Coach.git
cd AI-Real-Time-GYM-Coach

# 2. Install dependencies
pip install -r requirements.txt

# 3. Add your Groq API key
echo "GROQ_API_KEY=your_key_here" > .env

# 4. Run the app
streamlit run main.py
```

Open `http://localhost:8501` in your browser, log in, set your workout plan in the sidebar, and hit **Start Workout**.

---

## 🤝 Contributing

Contributions are welcome! Feel free to open an issue or submit a pull request for new exercises, UI improvements, or additional coaching logic.

---

## 👤 Author

**Yuvraj Rathore**
[GitHub](https://github.com/yuvrajrathore672)

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).
