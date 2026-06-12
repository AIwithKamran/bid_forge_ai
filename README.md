# BidForge AI 🚀

**AI-Powered Bid & Proposal Response Engine**

An intelligent system for analyzing RFPs (Request for Proposals), matching organizational capabilities, and generating competitive bid proposals. Designed for the CUST Hackathon 2026, Problem #1 (TEKROWE).

---

## 📋 Table of Contents

- [Features](#features)
- [Project Structure](#project-structure)
- [Tech Stack](#tech-stack)
- [Setup & Installation](#setup--installation)
- [Running the Application](#running-the-application)
- [Environment Configuration](#environment-configuration)
- [API Documentation](#api-documentation)
- [Architecture](#architecture)
- [Key Services](#key-services)
- [Contributing](#contributing)

---

## ✨ Features

- **RFP Analysis**: Automatically extract and parse requirements from proposal documents
- **Capability Matching**: Match organizational capabilities against RFP requirements using hybrid search (dense embeddings + structured signals)
- **Compliance Checking**: Evaluate compliance with RFP criteria and identify gaps
- **Bid Scoring**: AI-powered bid scoring with win probability prediction
- **Proposal Generation**: Generate customized proposal text using LLM integration
- **Historical Bid Tracking**: Track and analyze bid history with win/loss metrics
- **DOCX Export**: Export proposals as formatted Word documents
- **Demo Mode**: Fallback mode with cached responses for offline testing
- **Hybrid Search**: Combined dense vector search + keyword/structured matching for robust retrieval

---

## 📁 Project Structure

```
BidForge AI/
├── app/                                    # Backend FastAPI application
│   ├── main.py                            # FastAPI entry point
│   ├── models/
│   │   └── schemas.py                     # Pydantic data models
│   ├── routers/
│   │   ├── bid_history.py                 # Bid tracking endpoints
│   │   ├── capabilities.py                # Capability library management
│   │   ├── settings.py                    # Configuration endpoints
│   │   └── workspaces.py                  # Workspace management
│   ├── services/
│   │   ├── bid_history.py                 # Bid history logic
│   │   ├── capability_store.py            # FAISS vector store (embeddings)
│   │   ├── compliance_matcher.py          # RFP compliance evaluation
│   │   ├── criteria_taxonomy.py           # Criterion matching logic
│   │   ├── document_parser.py             # PDF/DOCX parsing
│   │   ├── docx_exporter.py               # Proposal DOCX generation
│   │   ├── faiss_store.py                 # FAISS index management
│   │   ├── llm_fallback.py                # LLM fallback logic (DEMO mode)
│   │   ├── ner_extractor.py               # Named entity recognition
│   │   ├── proposal_generator.py          # Proposal text generation
│   │   ├── requirement_extractor.py       # RFP requirement extraction
│   │   ├── scoring_engine.py              # Bid scoring algorithm
│   │   └── win_model.py                   # Win probability model
│   └── utils/
│       ├── llm_cache.py                   # LLM response caching
│       └── supabase_client.py             # Supabase integration
├── frontend/                               # React + Vite UI
│   ├── src/
│   │   ├── App.jsx                        # Main app component
│   │   ├── main.jsx                       # React entry point
│   │   ├── pages/                         # Page components
│   │   ├── components/                    # Reusable components
│   │   └── hooks/                         # Custom React hooks
│   ├── index.html                         # HTML template
│   ├── vite.config.js                     # Vite configuration
│   ├── tailwind.config.js                 # Tailwind CSS config
│   └── package.json                       # Frontend dependencies
├── scripts/                                # Utility scripts
│   ├── enrich_capabilities.py             # Capability library enrichment
│   ├── warm_cache.py                      # Warm LLM cache
│   ├── generate_project_report.py         # Project documentation
│   └── ...                                # Other analysis scripts
├── app/data/                              # Data directory
│   ├── capability_library_enriched.json   # Enriched capabilities
│   ├── criteria_taxonomy.json             # RFP criteria taxonomy
│   ├── bid_history.csv                    # Historical bid data
│   └── cache/                             # LLM response cache
├── requirements.txt                       # Python dependencies
├── schema.sql                             # Database schema
└── README.md                              # This file
```

---

## 🛠 Tech Stack

### Backend
- **FastAPI** (0.136.3) - Modern async web framework
- **Uvicorn** (0.49.0) - ASGI server
- **Pydantic** (2.13.4) - Data validation
- **LangChain** - LLM orchestration & composition
  - `langchain-groq` - Groq LLM integration
  - `langchain-openai` - OpenAI integration
- **Groq** (0.37.1) - Fast LLM inference
- **OpenAI** (2.41.1) - GPT models
- **FastEmbed** (0.8.0) - Fast embeddings (all-MiniLM-L6-v2 ONNX)
- **FAISS** (1.14.2) - Vector search index
- **Supabase** (2.31.0) - Backend-as-a-service
- **PyPDF** - PDF parsing
- **python-docx** - DOCX generation
- **Pandas** & **NumPy** - Data processing
- **scikit-learn** - ML utilities
- **ONNX Runtime** - Model inference

### Frontend
- **React** (18+) - UI library
- **Vite** - Build tool & dev server
- **Tailwind CSS** - Utility-first CSS
- **React Router** - Client-side routing

### Database
- **Supabase (PostgreSQL)** - Cloud database
- **SQLAlchemy** - ORM support
- Local CSV/JSON fallback for development

---

## 🚀 Setup & Installation

### Prerequisites
- **Python 3.12+** (3.14+ RC may have compatibility issues with Pydantic)
- **Node.js** (16+)
- **npm** or **yarn**
- Virtual environment (venv/virtualenv recommended)

### Backend Setup

1. **Clone/navigate to the project:**
   ```bash
   cd "d:\BidForge AI"
   ```

2. **Create and activate a Python virtual environment:**
   ```bash
   # Using Python 3.12 (recommended for compatibility)
   py -3.12 -m venv .venv312
   
   # Activate (Windows)
   .\.venv312\Scripts\activate
   
   # Activate (macOS/Linux)
   source .venv312/bin/activate
   ```

3. **Install Python dependencies:**
   ```bash
   pip install --upgrade pip
   pip install -r requirements.txt
   ```

### Frontend Setup

1. **Navigate to frontend directory:**
   ```bash
   cd frontend
   ```

2. **Install Node dependencies:**
   ```bash
   npm install
   ```

---

## ▶️ Running the Application

### Option 1: Run Both Services (Recommended)

**Terminal 1 - Backend:**
```bash
cd "d:\BidForge AI"
.\.venv312\Scripts\activate
python -m uvicorn app.main:app --reload --host 127.0.0.1 --port 8000
```

**Terminal 2 - Frontend:**
```bash
cd "d:\BidForge AI\frontend"
npm run dev -- --host 127.0.0.1 --port 5173
```

### Access the Application

- **Frontend**: http://127.0.0.1:5173/
- **Backend API**: http://127.0.0.1:8000/
- **API Docs (Swagger)**: http://127.0.0.1:8000/docs
- **API Docs (ReDoc)**: http://127.0.0.1:8000/redoc

---

## ⚙️ Environment Configuration

Create a `.env` file in the project root:

```env
# LLM Configuration
GROQ_API_KEY=your_groq_key_here
OPENAI_API_KEY=your_openai_key_here

# Supabase Configuration
SUPABASE_URL=https://your-project.supabase.co
SUPABASE_KEY=your_supabase_anon_key

# Application Settings
DEBUG=false              # Enable debug endpoints
DEMO_MODE=false          # Use cached responses instead of live LLM calls
MANUAL_BASELINE_HOURS=0  # Manual time baseline override

# Embedding Cache
HF_TOKEN=                # Optional: Hugging Face token for faster model downloads
```

### Key Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `DEBUG` | `false` | Enable debug endpoints (hybrid search inspector) |
| `DEMO_MODE` | `false` | Use cached LLM responses, skip heavy computation |
| `MANUAL_BASELINE_HOURS` | `0` | Override time baseline for win model |
| `GROQ_API_KEY` | (required) | API key for Groq LLM |
| `OPENAI_API_KEY` | (optional) | API key for OpenAI GPT models |

---

## 📡 API Documentation

### Core Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/health` | Health check & service status |
| `GET` | `/docs` | Interactive API documentation (Swagger) |
| `GET` | `/redoc` | ReDoc API documentation |

### Workspaces
- `POST /api/workspaces` - Create workspace
- `GET /api/workspaces` - List workspaces

### Bid Analysis
- `POST /api/analyze` - Analyze RFP and generate bid
- `GET /api/bids` - List bid history
- `GET /api/bids/{bid_id}` - Get bid details

### Capabilities
- `GET /api/capabilities` - List capabilities
- `POST /api/capabilities/upload` - Upload capability library
- `GET /api/capabilities/search` - Search capabilities

### Settings
- `GET /api/settings` - Get current settings
- `PATCH /api/settings` - Update settings (DEBUG, DEMO_MODE, etc.)

---

## 🏗 Architecture

### Request Flow

```
User Request
    ↓
Frontend (React/Vite)
    ↓
FastAPI Backend
    ├─→ Document Parser (PDF/DOCX)
    ├─→ Requirement Extractor (NER + LLM)
    ├─→ Capability Store (FAISS Vector Search)
    ├─→ Compliance Matcher (LLM Evaluation)
    ├─→ Scoring Engine (ML + Heuristics)
    ├─→ Win Model (LogisticRegression)
    └─→ Proposal Generator (LLM + Streaming)
    ↓
Response + Export (DOCX)
```

### Key Components

1. **Capability Store** - FAISS-based vector search with hybrid matching
2. **Document Parser** - Extract text from RFP documents
3. **Requirement Extractor** - Identify and structure RFP requirements
4. **Compliance Matcher** - Evaluate capability compliance with criteria
5. **Scoring Engine** - Calculate bid attractiveness and win probability
6. **Proposal Generator** - Generate proposal text using LLM
7. **LLM Cache** - Cache responses for performance & cost reduction
8. **Demo Mode** - Fallback mode with pre-cached responses

---

## 🔧 Key Services

### `capability_store.py`
Manages the capability library using FAISS vector search:
- Hybrid search: dense embeddings + structured matching
- FastEmbed (all-MiniLM-L6-v2) for text embeddings
- Library reload capability

### `proposal_generator.py`
Generates proposal text using LLM:
- Streaming response support
- Cached fallback in DEMO_MODE

### `scoring_engine.py`
Calculates bid scores:
- Win probability prediction
- Historical performance weighting
- Time-based adjustments

### `llm_fallback.py`
Handles LLM failures gracefully:
- Retry logic with backoff
- Cached response fallback
- Demo mode support

---

## 📝 Environment Setup Notes

### Python Version Compatibility
- **Recommended**: Python 3.12 (fully tested)
- **Avoid**: Python 3.14-RC (Pydantic compatibility issues with `_eval_type()`)
- **Supported**: Python 3.11, 3.13

### Virtual Environment
Use `.venv312` for Python 3.12 compatibility:
```bash
py -3.12 -m venv .venv312
.\.venv312\Scripts\activate
```

### First Run Performance
On first run, the backend will:
1. Download the FastEmbed model (~650MB)
2. Load the capability library
3. Build the FAISS index
4. Train the win probability model

This may take 2-5 minutes. Subsequent runs are faster.

---

## 🤝 Contributing

1. Create a feature branch: `git checkout -b feature/my-feature`
2. Make your changes
3. Test thoroughly
4. Commit with clear messages: `git commit -m "Add feature description"`
5. Push and create a pull request

---

## 📄 License

Part of CUST Hackathon 2026, Problem #1 (TEKROWE)

---

## 📞 Support

For issues or questions:
- Check the `.env.example` file for configuration templates
- Review API documentation at `/docs` endpoint
- Check `scripts/` directory for utility scripts
- Refer to `app/services/` for service documentation

---

## 🎯 Roadmap

- [ ] Docker containerization
- [ ] Kubernetes deployment
- [ ] Advanced analytics dashboard
- [ ] Multi-language support
- [ ] Extended LLM provider support
- [ ] Real-time collaboration features

---

**Last Updated**: June 2026
