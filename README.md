# 🎥 YouTube/Podcast RAG Assistant

An intelligent, AI-powered Q&A system that allows users to "chat" with long-form audio and video content. Paste a YouTube link, and the system transcribes the audio, indexes the meaning of the content, and answers your questions with exact timestamp citations.

## 🚀 The Problem
Traditional search only finds keywords. If you watch a 2-hour podcast, finding a specific topic requires scrubbing through the video manually. Context windows of LLMs are too small to process an entire 2-hour transcript at once.

## 💡 The Solution
This project implements a **RAG (Retrieval-Augmented Generation)** pipeline. It breaks the transcript into small chunks, converts them into mathematical vectors (embeddings), and stores them in a local vector database. When a user asks a question, the system finds the most relevant chunks and feeds them to an LLM to generate a factual answer with timestamps.

## ✨ Features
- **Audio Extraction:** Downloads audio directly from YouTube URLs.
- **Speech-to-Text:** Transcribes audio locally using OpenAI's Whisper model.
- **Semantic Search:** Uses `Sentence Transformers` to find context based on *meaning*, not just exact keywords.
- **Vector Database:** Stores transcript chunks locally using `ChromaDB` for lightning-fast retrieval.
- **Timestamp Citations:** The LLM answers the question and tells you exactly *when* in the video the topic was discussed.
- **Clean UI:** Built with `Streamlit` for a smooth, browser-based user experience.

## 🛠️ Tech Stack
- **Language:** Python
- **Backend:** FastAPI (or Streamlit for the UI layer)
- **Speech-to-Text:** OpenAI Whisper
- **NLP & Embeddings:** Sentence Transformers (`all-MiniLM-L6-v2`)
- **Vector Database:** ChromaDB
- **LLM Engine:** Groq API (Llama 3)
- **UI:** Streamlit
- **Audio Downloader:** yt-dlp

## 🏗️ Architecture Pipeline

1. **Ingestion:** User inputs a YouTube URL.
2. **Transcription:** `yt-dlp` downloads the audio, and `Whisper` converts it to a timestamped JSON transcript.
3. **Chunking:** The transcript is split into overlapping 500-word chunks to preserve context.
4. **Embedding:** Each chunk is converted into a vector using `Sentence Transformers`.
5. **Storage:** Vectors and timestamps are saved in `ChromaDB`.
6. **Querying:** User asks a question -> Question is embedded -> ChromaDB retrieves the top 3 most similar chunks -> LLM (Groq) reads those chunks and generates the final answer.

*(Optional: Add a simple Mermaid.js diagram here later if you want to look extra professional)*

## 📦 Installation & Setup

1. **Clone the repository:**
   ```bash
   git clone https://github.com/yourusername/youtube-rag-assistant.git
   cd youtube-rag-assistant
   
python -m venv venv
**On Windows:**
venv\Scripts\activate
**On Mac/Linux:**
source venv/bin/activate
pip install -r requirements.txt


GROQ_API_KEY=your_groq_api_key_here

streamlit run app.py
