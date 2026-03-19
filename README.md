# 🎬 Video Analysis & Summarization

This project extracts frames and audio from a video, generates captions using AI vision models, transcribes speech, and summarizes the content into concise text.  
It combines **FastAPI** for the backend, **Streamlit** for the frontend, and integrates **OpenAI** + **Hugging Face Llama vision** model for AI-powered video understanding.

---

## 🚀 Features
- 📽️ **Video Upload**: Upload MP4 or other video formats via Streamlit frontend.
- 🖼️ **Frame Captioning**: Extracts video frames and generates captions with OpenAI Vision / Hugging Face models.
- 🎙️ **Audio Transcription**: Converts video audio to text using Whisper.
- 📝 **Summarization**: Produces a concise summary of the video using LLMs.
- 🌐 **API + Web UI**: 
  - FastAPI backend (`/summarize_video` endpoint).  
  - Streamlit frontend for user interaction.
- 🐳 **Dockerized**: Runs in a container for reproducibility.
- ☁️ **Colab GPU Ready**: Can run on Google Colab with GPU support.

---

## ⚙️ Working of the Project

Here’s how the project processes a video step by step:

1. **Video Upload**  
   - User uploads a video through the **Streamlit frontend**.  
   - The video is sent to the **FastAPI backend** for processing.  

2. **Frame Extraction**  
   - Frames are extracted from the video at fixed intervals using **MoviePy / FFmpeg**.  
   - Example: 1 frame every 2 seconds of video.  

3. **Frame Captioning**  
   - Each extracted frame is passed to **GPT-4 Vision** (or a Hugging Face Vision model).  
   - The model generates a detailed **caption/description** for the frame.  

4. **Audio Extraction & Transcription**  
   - The audio is separated from the video (using MoviePy).  
   - Audio is transcribed into text using **Whisper** (speech-to-text).  

5. **Content Fusion**  
   - Captions (visual descriptions) + Transcript (spoken text) are combined.  
   - This creates a **rich multimodal representation** of the video.  

6. **Summarization**  
   - Combined text is passed to an **LLM (OpenAI GPT / Hugging Face summarizer)**.  
   - Produces a **concise summary** highlighting key points of the video.  

7. **Result Delivery**  
   - The final summary is sent back to the **frontend (Streamlit)**.  
   - User sees the summary text, and optionally can download it.  

---

## 📂 Project Structure
video_summarization/
│── app.py # Streamlit frontend
│── main.py # FastAPI backend
│── requirements.txt # Python dependencies
│── Dockerfile # Build container image
│── .env # Environment variables (ignored by Git)
│── summerizer.py # Helper scripts (frame extraction, audio, etc.)
│── .gitignore # Ignore secrets & unnecessary files


---

## ⚙️ Setup Instructions

### 🔑 1. Environment Variables
- Create a `.env` file in the project root:
- OPENAI_API_KEY=your_openai_api_key_here

###    2. Local Installation (GPU only)
- git clone [https://github.com/hakazmi/Video-Analysis-Summarization.git]
- cd Video-Analysis-Summarization

### Create virtual environment
- python -m venv venv
- source venv/bin/activate  # (On Windows: venv\Scripts\activate)

### Install dependencies
- pip install -r requirements.txt

### Run backend (FastAPI):
- uvicorn main:app --host 0.0.0.0 --port 8000
  
### Run frontend (Streamlit):
- streamlit run app.py --server.port 8501
###    3. Run with Docker (Recommended)
### Build the image
- docker build -t video-summarizer .

### Run container
- docker run -p 8000:8000 -p 8501:8501 --env-file .env video-summarizer

  ### Now access:
- Backend: http://localhost:8000/docs
- Frontend: http://localhost:8501

### 🧠 Models Used

- Llama Vision → Frame captioning & summarization.

- Whisper (OpenAI/Hugging Face) → Audio transcription.

- OpenAI GPT-4 → summarization models.

   

