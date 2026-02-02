# MindMate MVP 🧠

**MindMate** is a compassionate AI mental wellness companion designed to support college students. It offers a safe space to talk, track moods, and gain insights into emotional well-being.

## 🚀 Features

- **Empathetic AI Chat**: Talk to a supportive AI (powered by Groq/Gemini) that remembers context.
- **Mood Tracking**: Log your daily emotions with a simple emoji interface.
- **Analytics Dashboard**: Visualize your mood trends over time.
- **Crisis Support**: Automatic detection of distress keywords with immediate helpline resources.
- **Secure**: Private conversations and user data protection.

## 🛠️ Tech Stack

- **Frontend**: React, Vite, Chart.js
- **Backend**: FastAPI, Python
- **Database**: Firebase Firestore
- **AI**: Groq, Google Gemini, OpenAI

## 🏁 Quick Start

### Prerequisites
- Node.js & npm
- Python 3.10+
- Firebase Project

### 1. Backend Setup
```bash
cd backend
python -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows
pip install -r requirements.txt
cp .env.example .env      # Add your API keys
python main.py
```

### 2. Frontend Setup
```bash
cd frontend
npm install
cp .env.example .env      # Add your Firebase config
npm run dev
```

Visit -> `http://localhost:5173` to start using MindMate!!

## 📚 Documentation

- [Implementation Details](docs/IMPLEMENTATION.md)
- [Setup Guide](docs/SETUP_GUIDE.md)
- [Architecture](docs/ARCHITECTURE.md)
- [API Reference](docs/API_REFERENCE.md)
- [Testing Guide](docs/TESTING_GUIDE.md)

## 📄 License

MIT
