
# 🤖 LISA - AI Meeting Assistant

**LISA (Live Intelligent Speech Analysis)** is an AI-powered assistant that enhances meeting productivity by automatically transcribing recordings, summarizing content, extracting action items, and enabling semantic search.

---

## 🚀 Features

- 🎙 **Transcription** — Converts meeting audio/video to text using OpenAI's Whisper API  
- 📝 **Meeting Minutes** — Summarizes meetings into concise bullet points   
- 🔍 **Semantic Search** — Find key information in transcripts with natural language queries  
- 🧠 **Vector Storage** — Uses ChromaDB for fast, persistent retrieval of embedded transcript data  

---

## ⚙️ How It Works

1. **Audio Extraction**: Pulls audio from uploaded video files  
2. **Transcription**: Uses Whisper API to convert speech to timestamped text  
3. **Analysis**: Generates meeting summaries   
4. **Embedding & Indexing**: Chunks and vectorizes transcript using OpenAI embeddings  
5. **Storage**: Persists vectors in ChromaDB  
6. **Retrieval**: Answers semantic queries using vector search  

---

## 🔧 Backend Setup

### 📦 Prerequisites

- Python 3.8+
- [Poetry](https://python-poetry.org/docs/#installation)
- OpenAI API Key

### 🧪 Installation

```bash
# Clone the backend repository
git clone <your-backend-repo-url>
cd lisa-backend

# Install dependencies
poetry install
```

### 🔐 Set Environment Variable

#### Option 1: Export directly

```bash
export OPENAI_API_KEY=your-api-key       # macOS/Linux
set OPENAI_API_KEY=your-api-key          # Windows
```

#### Option 2: Use a `.env` file

```env
OPENAI_API_KEY=your-api-key
```

---

### ▶️ Run the Server

```bash
poetry run start
```

Server runs at: `http://localhost:8000`

---

## 🛰 API Endpoints

| Method | Endpoint           | Description                                   |
|--------|--------------------|-----------------------------------------------|
| POST   | `/predict`         | Upload video and get transcript & summary     |
| GET    | `/results/{job_id}`| Retrieve results by job ID                    |
| POST   | `/search`          | Semantic search on transcripts                |

---

### 📦 Example: Process a Meeting Video

```python
import requests
import base64

with open("meeting.mp4", "rb") as f:
    video_base64 = base64.b64encode(f.read()).decode("utf-8")

response = requests.post(
    "http://localhost:8000/predict",
    json={"video": f"data:video/mp4;base64,{video_base64}"}
)

print(response.json()["job_id"])
```

---

### 🔎 Example: Search Meeting Transcript

```python
import requests

response = requests.post(
    "http://localhost:8000/search",
    json={"job_id": "your-job-id", "query": "project deadline"}
)

print(response.json())
```

---

## 🌐 Frontend (LISA App – Next.js)

A sleek web UI for uploading meetings, browsing transcripts, and using semantic search.

### 📦 Prerequisites

- Node.js v14+
- Yarn (`npm install -g yarn`)

### 💻 Installation

```bash
# Clone the frontend repo
git clone <your-frontend-repo-url>
cd lisa-app

# Install dependencies
yarn install
```

### ▶️ Start Development Server

```bash
yarn dev
```

Open browser at: [http://localhost:3000](http://localhost:3000)

---

## 📁 Project Structure

```
lisa-app/
├── pages/          # Route and API handlers
├── components/     # Reusable React components
├── styles/         # CSS modules and global styles
├── utils/          # Utility functions
├── public/         # Static assets
```

---

## 🛠 Useful Scripts

| Script       | Description                  |
|--------------|------------------------------|
| `yarn dev`   | Starts development server    |
| `yarn build` | Builds app for production    |
| `yarn start` | Runs built app               |
| `yarn export`| Exports static HTML version  |

---

## 📚 Learn More

- [Next.js Docs](https://nextjs.org/docs)
- [OpenAI Whisper](https://openai.com/research/whisper)
- [ChromaDB](https://www.trychroma.com/)
- [Poetry](https://python-poetry.org/)


