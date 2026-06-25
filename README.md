<h1 align="center">InstaViral AI</h1>

<p align="center">
  <b>Intelligent Video Analyzer and Content Optimizer for Instagram Reels</b><br/>
  AI-powered virality analysis · Multilingual feedback · Groq-powered pipeline
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10%2B-blue?style=flat-square&logo=python" />
  <img src="https://img.shields.io/badge/FastAPI-backend-green?style=flat-square&logo=fastapi" />
  <img src="https://img.shields.io/badge/Streamlit-frontend-red?style=flat-square&logo=streamlit" />
  <img src="https://img.shields.io/badge/MongoDB-Atlas-brightgreen?style=flat-square&logo=mongodb" />
  <img src="https://img.shields.io/badge/Groq-AI%20Models-orange?style=flat-square" />
  <img src="https://img.shields.io/badge/License-MIT-lightgrey?style=flat-square" />
</p>

---

## What is InstaViral AI?

InstaViral AI is a full-stack AI application that helps Indian Instagram Reels
creators understand **why their videos aren't going viral** — and exactly what to fix.

Instead of generic advice, the system breaks the video apart, measures 14 key
viral signals (hook strength, audio sentiment, visual energy, emotion, editing pace,
and more), computes a **Virality Score out of 100** by comparing against real viral
benchmarks, and delivers a detailed improvement report in **Hindi, Marathi, or English**.

---

## The Problem

- Instagram Reels has 500M+ monthly active users in India.
- Most Reels receive fewer than 1,000 views.
- Creators have no specific data on what is wrong — generic advice like
  "post more consistently" does not help.
- There is no tool that analyzes the actual video and gives hyper-specific,
  language-aware feedback grounded in real viral benchmarks.

---

## Key Features

- **Multi-modal AI analysis** — audio transcription, visual frame analysis,
  facial emotion detection, and structural video metrics in one pipeline.
- **14 viral signal measurement** — hook strength, audio sentiment, CTA presence,
  visual energy, lighting, composition, color vibrancy, on-screen text,
  positive emotion, smile ratio, emotional variance, cuts per minute,
  motion intensity, and background music.
- **Virality Score (0–100)** — computed using cosine similarity against
  a database of known viral videos.
- **AI-generated improvement report** — specific suggestions, optimized caption,
  relevant hashtags, and ideal posting time.
- **Multilingual output** — auto-detects the creator's language and responds
  in Hindi, Marathi, or English.
- **Video link support** — accepts direct uploads or a URL (yt-dlp powered).

---

## Tech Stack

| Layer            | Technology                  | Purpose                                          |
|------------------|-----------------------------|--------------------------------------------------|
| Frontend         | Streamlit + Plotly          | Upload page and interactive results dashboard    |
| Backend          | FastAPI + Uvicorn           | REST API server orchestrating the AI pipeline    |
| Database         | MongoDB Atlas               | Stores jobs, results, and benchmark video data   |
| Speech-to-Text   | Groq Whisper Large V3       | Transcribes spoken audio from the video          |
| Vision AI        | Groq Llama 4 (multimodal)   | Analyzes video frames for energy and composition |
| Suggestion AI    | Groq Llama 3.3-70B          | Generates the human-readable improvement report  |
| Emotion Analysis | EmotiEffLib + MediaPipe     | Face detection and expression scoring            |
| Scene Detection  | PySceneDetect               | Identifies editing cut points                    |
| Video Processing | OpenCV + moviepy + FFmpeg   | Frame extraction, audio splitting, motion stats  |
| Scoring          | scikit-learn cosine similarity | Compares user video against viral benchmarks  |
| Video Download   | yt-dlp                      | Downloads reference videos from URLs             |

---

## System Architecture

```
User (Upload / URL)
        |
   Streamlit Frontend
        |
   FastAPI Backend  ─────────────────────────────────┐
        |                                             |
   ┌────┴─────────────────────────────┐        MongoDB Atlas
   │         Analysis Pipeline        │     (jobs / results /
   │                                  │      benchmarks)
   │  Audio ──► Whisper (transcript,  │
   │             sentiment, hook)     │
   │                                  │
   │  Frames ─► Llama 4 (visual       │
   │             energy, composition) │
   │                                  │
   │  Faces ──► EmotiEffLib           │
   │            (emotion, smiles)     │
   │                                  │
   │  Motion ─► OpenCV / PySceneDetect│
   │            (cuts/min, intensity) │
   └────────────────┬─────────────────┘
                    │
         14-dim Feature Vector
                    │
         Cosine Similarity Scoring
                    │
         Virality Score (0–100)
                    │
         Gap Analysis + Holistic Review
                    │
         Llama 3.3-70B → Improvement Report
         (caption, hashtags, posting time, tips)
                    │
        Streamlit Results Dashboard
```

---

## The 14 Viral Signals

| Category  | Signals                                                              |
|-----------|----------------------------------------------------------------------|
| Audio     | Speech sentiment, hook strength (first 3 sec), CTA presence         |
| Visual    | Visual energy, lighting, composition, color vibrancy, on-screen text|
| Emotion   | Positive emotion, emotional variance, smile ratio                    |
| Structure | Cuts per minute, motion intensity, background music present          |

Each signal is normalized to a value between 0 and 1, combined into a
14-dimensional vector, and compared against viral benchmark vectors using
cosine similarity.

---

## Getting Started

### Prerequisites

- Python 3.10+
- FFmpeg installed and available in PATH
- MongoDB Atlas connection string
- Groq API key

### Installation

```bash
# Clone the repository
git clone https://github.com/your-username/instavirus-ai.git
cd instavirus-ai

# Create a virtual environment
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### Configuration

Create a `.env` file in the project root:

```env
GROQ_API_KEY=your_groq_api_key_here
MONGODB_URI=your_mongodb_atlas_connection_string
DATABASE_NAME=instavirus_db
```

### Running the Application

```bash
# Start the FastAPI backend
uvicorn app.main:app --reload --port 8000

# In a separate terminal, start the Streamlit frontend
streamlit run frontend/app.py
```

Open your browser at `http://localhost:8501` to access the application.

---

## Project Structure

```
instavirus-ai/
├── app/
│   ├── main.py              # FastAPI entry point
│   ├── analyzer.py          # Core video analysis pipeline (conductor)
│   ├── audio_analysis.py    # Whisper transcription + sentiment
│   ├── vision_analysis.py   # Llama 4 frame analysis
│   ├── emotion_analysis.py  # EmotiEffLib + MediaPipe face scoring
│   ├── scoring.py           # Feature vector + cosine similarity
│   └── report_generator.py  # Llama 3.3-70B suggestion generation
├── frontend/
│   └── app.py               # Streamlit upload + results UI
├── benchmarks/              # Viral reference video vectors
├── requirements.txt
├── .env.example
└── README.md
```

---

## Applications

- Instagram Reels content optimization for individual creators
- Influencer growth strategy and data-driven audience targeting
- Social media marketing campaign quality testing
- Brand promotion and product advertisement optimization
- Automated multilingual caption and hashtag generation

---

## Limitations

- Virality Score accuracy depends on the quality and size of the benchmark dataset.
- Instagram trend patterns change rapidly; periodic retraining improves results.
- Currently supports Instagram Reels only.
- Processing time increases with high-resolution or long-duration videos.

---

## Future Scope

- Support for YouTube Shorts, TikTok, Moj, and Josh
- Real-time analysis during video recording
- Mobile app for Android and iOS
- AI-generated thumbnails and video titles
- Automatic script and voice-over generation
- Cloud deployment on AWS / GCP with user authentication

---

## Research Foundation

This project builds on published research in multimodal video popularity prediction:

- He, Z. & Li, D. (2024). *Short Video Popularity Prediction using AI and Deep Learning* — CPRP-CNN model, 74.7% accuracy.
- Rivadeneira, L. & Loor, I. (2024). *Evidential Reasoning Approach for Predicting Popularity of Instagram Posts* — MAKER model, textual + visual features.
- Bielski, A. & Trzcinski, T. (2018). *Multimodal Popularity Prediction with Self-Attention* — frames + text combined analysis.

---

## Team

| Name                    | Roll No.    |
|-------------------------|-------------|
| Dnyaneshwari Dandagawhal | 72249220M  |
| Shravani Jadhav          | 72249281C  |
| Shubham Ghodele          | 72249253H  |
| Vaishnavi Maske          | 72249332M  |

**Internal Guide:** Prof. Madhuri Kale  
**Institution:** Dhole Patil College of Engineering, Pune  
**Department:** Computer Engineering · Group ID: 014

---

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.

