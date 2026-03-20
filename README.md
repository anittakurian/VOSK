# **VOSK**

## **Folder Structure**

railway-assistant/  
│── app.py                  \# CLI entry point  
│── pipeline.py             \# Core orchestrator connecting all modules  
│── requirements.txt  
│── README.md  
│  
├── core/  
│   ├── speech.py           \# Speech Recognition \+ Translation 
│   ├── nlp.py              \# Intent Detection \+ Entity Extraction
│   ├── output.py           \# Final translation \+ Speech synthesis 
│   └── train\_service.py    \# Railway data handler (Mocked NTES route)  
│  
└── (future folders: models/, config/, docs/)

## **System Data Flow**

USER SPEECH/TEXT  
      ↓  
SpeechUnit  ──────────────────►  Converts speech → text \+ detects language  
      ↓  
NLPDecisionUnit  ─────────────►  Extracts intent \+ entities (train number, etc.)  
      ↓  
TrainService  ────────────────►  Fetches route/data  
      ↓  
OutputUnit  ──────────────────►  Formats \+ translates response  
      ↓  
FINAL RESPONSE

## **Quick Start**

**Install Dependencies:**  
pip install \-r requirements.txt

**Run the Application:**  
python app.py

## **Development Workflow**

| Action | Command |
| :---- | :---- |
| Create feature branch | git checkout \-b feature/module-name |
| Stage changes | git add . |
| Commit | git commit \-m "feat: improved NLP intent extractor" |
| Push | git push |
| Open PR | via GitHub |

## **🧩 Module Responsibilities**

| Module | Responsibilities | Swappable Later | Status |
| :---- | :---- | :---- | :---- |
| **speech.py** | Language detection, STT, translation | ✔ Whisper / Indic model | Complete |
| **nlp.py** | Intent detection \+ entity extraction | ✔ HF transformers / finetuned model | Complete |
| **train\_service.py** | Get train info via API or scraping | ✔ Real NTES API | Mocked |
| **output.py** | Translation \+ TTS output | ✔ Google TTS / Coqui TTS | Complete |
| **pipeline.py** | Orchestration, error handling, data flow | ❌ Core logic | Functional |

## **Contribution Guidelines**

You are modifying a module inside a modular AI pipeline.  
**Rules:**

1. **Do NOT** remove or rename public function names.  
2. Maintain data formats expected by pipeline.py.  
3. Add improvements internally (real STT, NLP, API calls, TTS, caching etc.).  
4. Use clean logging for debugging.  
5. Do not break the pipeline flow.

