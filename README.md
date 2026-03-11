# 🧠 Therapy AI — Enterprise-Grade AI Training Platform

> **A production-ready, full-stack AI application for therapy training with dual LLM support, real-time WebSocket communication, and advanced security features.**

[![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=flat&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![Next.js](https://img.shields.io/badge/Next.js-15-black?style=flat&logo=next.js&logoColor=white)](https://nextjs.org/)
[![Node.js](https://img.shields.io/badge/Node.js-20-green?style=flat&logo=node.js&logoColor=white)](https://nodejs.org/)
[![Express](https://img.shields.io/badge/Express-4.x-gray?style=flat&logo=express&logoColor=white)](https://expressjs.com/)

---

## 🎯 Project Overview

**Therapy AI** is a sophisticated, production-ready platform that enables medical students and practitioners to practice therapeutic skills with AI-powered personas. Built with enterprise-grade architecture, it demonstrates advanced full-stack development, real-time systems, AI/ML integration, and security best practices followed by AI practices.

### Key Highlights

- ✅ **Production-Ready**: SQLite persistence, rate limiting, security headers, structured logging
- ✅ **Dual LLM Architecture**: Seamless switching between Google Gemini (cloud) and Ollama (local)
- ✅ **Real-Time Communication**: WebSocket-based bidirectional chat with session management
- ✅ **AI Persona Generation**: Upload therapy case documents (PDF/DOCX) to generate custom AI personas
- ✅ **Enterprise Security**: Input validation, sanitization, rate limiting, helmet.js protection
- ✅ **Scalable Architecture**: Modular service design with fallback mechanisms

---

## 🚀 Technical Achievements

### Production-Ready Features

| Feature | Implementation | Impact |
|---------|---------------|--------|
| **Persistent Storage** | SQLite with ACID transactions | Zero data loss on server restarts |
| **Rate Limiting** | 100 req/15min per IP with express-rate-limit | DDoS protection, abuse prevention |
| **Security Headers** | Helmet.js (XSS, CSRF, clickjacking protection) | Enterprise-grade security |
| **Structured Logging** | JSON-formatted logs with levels (info/warn/error) | Production monitoring & debugging |
| **Input Validation** | Middleware-based sanitization & validation | Injection attack prevention |
| **Error Handling** | Comprehensive error boundaries with user-friendly messages | Improved UX & reliability |

### Architecture Highlights

- **Dual LLM Provider System**: Abstracted provider pattern allowing runtime switching between cloud (Gemini) and local (Ollama) LLMs
- **WebSocket Real-Time Engine**: Persistent connections with keep-alive, session management, and graceful error handling
- **Document Processing Pipeline**: Multi-format support (PDF/DOCX) with AI-powered persona extraction
- **Modular Service Architecture**: Interface-based design with fallback chains (SQLite → GCS → In-Memory)
- **Type-Safe Development**: Full TypeScript coverage across frontend and backend

---

## 🏗️ Technology Stack

### Frontend
- **Next.js 15** with App Router - Modern React framework with server-side rendering
- **React 18** - Component-based UI with hooks and context
- **TypeScript** - Type-safe development with strict mode
- **Tailwind CSS** - Utility-first responsive design
- **WebSocket API** - Real-time bidirectional communication
- **SpeechSynthesis API** - Browser-based text-to-speech

### Backend
- **Node.js 20** - JavaScript runtime
- **Express.js** - RESTful API framework
- **TypeScript** - Full type safety
- **WebSocket (ws)** - Real-time WebSocket server
- **SQLite (better-sqlite3)** - Persistent database with ACID transactions
- **Helmet.js** - Security headers middleware
- **express-rate-limit** - API rate limiting
- **Multer** - File upload handling
- **Mammoth** - DOCX document parsing
- **pdf-parse** - PDF text extraction

### AI & ML
- **Google Gemini 2.5 Flash** - Cloud-based LLM via API
- **Ollama (Llama 3)** - Local LLM for privacy-focused deployments
- **Custom Persona Generation** - AI-powered extraction from therapy case documents

### Infrastructure
- **Docker** - Containerization support
- **Vercel** - Frontend deployment ready
- **Railway** - Backend deployment ready
- **Environment-based Configuration** - Secure secrets management

---

## 📐 System Architecture

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        CLIENT LAYER (Frontend)                              │
│                                                                             │
│     ┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐       │
│     │   Next.js 15    │    │   WebSocket     │    │   React 18      │       │
│     │   App Router    │◄───┤   Client        │    │   Components    │       │
│     │  (Port 3000)    │    │  (Real-time)    │    │   + Hooks       │       │
│     └────────┬────────┘    └────────┬────────┘    └─────────────────┘       │
│              │                      │                                       │
│              └──────────────────────┴───────────────────────────────────────┘
└──────────────────────────────┬──────────────────────────────────────────────┘
                               │
                    ┌──────────┴──────────┐
                    │                     │
          HTTP/REST (Port 3001)    WebSocket (Port 8080)
                    │                     │
┌───────────────────▼─────────────────────▼─────────────────────────────────┐
│                      APPLICATION LAYER (Backend)                          │
│                                                                           │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐   │
│  │   Express    │  │  WebSocket   │  │   Auth       │  │  Middleware  │   │
│  │   REST API   │  │   Server     │  │   Service    │  │              │   │
│  │              │  │              │  │              │  │ Rate Limit   │   │
│  │ • Auth       │  │ • Sessions   │  │ • SQLite     │  │ Validation   │   │
│  │ • Personas   │  │ • Real-time  │  │ • GCS        │  │ Logging      │   │
│  │ • Health     │  │ • Keep-alive │  │ • Fallback   │  │              │   │
│  └──────┬───────┘  └──────┬───────┘  └──────┬───────┘  └──────────────┘   │
└─────────┼──────────────────┼────────────────┼──────────────────────────── ┘
          │                  │                │
          │                  │                │
┌─────────▼──────────────────▼────────────────▼──────────────────────────────┐
│                           SERVICE LAYER                                    │
│                                                                            │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐    │
│  │   LLM        │  │   SQLite     │  │   Document   │  │   Persona    │    │
│  │   Router     │  │   Database   │  │   Parser     │  │   Generator  │    │
│  │              │  │              │  │              │  │              │    │
│  │ • Gemini     │  │ • ACID       │  │ • PDF Parse  │  │ • AI Extract │    │
│  │ • Ollama     │  │ • Indexed    │  │ • DOCX Parse │  │ • Few-shot   │    │
│  │ • Lazy Init  │  │ • Persistent │  │ • Validation │  │ • JSON Store │    │
│  └──────┬───────┘  └──────────────┘  └──────────────┘  └──────────────┘    │
└─────────┼──────────────────────────────────────────────────────────────────┘
          │
          │
┌─────────▼───────────────────────────────────────────────────────────────────┐
│                        EXTERNAL SERVICES                                    │
│                                                                             │
│     ┌──────────────────────┐          ┌──────────────────────┐              │
│     │  Google Gemini API   │          │   Ollama (Local)     │              │
│     │                      │          │                      │              │
│     │ • Gemini 2.5 Flash   │          │ • Llama 3 Model      │              │
│     │ • Cloud-based        │          │ • Local Inference    │              │
│     │ • API Key Required   │          │ • Privacy-focused    │              │
│     └──────────────────────┘          └──────────────────────┘              │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Data Flow

```
User Input
    │
    ├─► WebSocket ──► Server ──► Crisis Detection
    │                              │
    │                              ├─► [Crisis] ──► Safety Response
    │                              │
    │                              └─► [Normal] ──► Persona Loader
    │                                                    │
    │                                                    ├─► System Prompt
    │                                                    ├─► Few-shot Examples
    │                                                    └─► Conversation History
    │                                                          │
    │                                                          ▼
    │                                                    LLM Router
    │                                                          │
    │                                                          ├─► Gemini API
    │                                                          │   (Cloud)
    │                                                          │
    │                                                          └─► Ollama HTTP
    │                                                              (Local)
    │                                                          │
    │                                                          ▼
    └─────────────────────────────────────────────────── AI Response
                                                              │
                                                              ▼
                                                    WebSocket ──► Frontend
                                                              │
                                                              ├─► UI Display
                                                              └─► Speech Synthesis
```

### Component Architecture

**Frontend (Next.js)**
- `TherapyAi.tsx` - Main therapy interface with WebSocket client, session management, and real-time chat
- `PractitionerDashboard.tsx` - Analytics dashboard with progress tracking and session insights
- `StudentDashboard.tsx` - Student-specific features with learning analytics
- `PersonaManagement.tsx` - Persona selection and management UI
- `PersonaUploadModal.tsx` - Document upload with AI-powered persona generation

**Backend (Node.js/Express)**
- `index.ts` - Main server orchestrating Express API and WebSocket server
- `llm.ts` - LLM provider router with lazy initialization and error handling
- `routes/auth.ts` - Authentication endpoints with SQLite persistence
- `routes/personas.ts` - Persona CRUD operations with file system integration
- `services/sqlite-auth.ts` - Production-grade authentication with ACID transactions
- `services/persona-generator.ts` - AI-powered persona generation from documents
- `services/document-parser.ts` - Multi-format document parsing (PDF/DOCX)
- `services/ollama-llm.ts` - Local LLM integration with health checks
- `middleware/validation.ts` - Input validation and sanitization
- `middleware/logger.ts` - Structured request/response logging
- `safety.ts` - Crisis detection system with keyword monitoring

---

## 🔄 How It Works

### 1. Authentication & User Management
- **SQLite Database**: Persistent user storage with email indexing
- **Password Hashing**: SHA-256 with secure storage
- **Role-Based Access**: Student and Practitioner dashboards
- **Session Management**: Secure session handling with last login tracking

### 2. Persona System
- **Pre-built Personas**: Sarah Chen (anxiety), Marcus Williams (depression), Elena Rodriguez (PTSD)
- **Custom Persona Generation**: 
  1. Upload therapy case document (PDF/DOCX)
  2. Document parsing and text extraction
  3. AI-powered persona extraction (demographics, concerns, personality)
  4. System prompt and few-shot example generation
  5. JSON storage in knowledge base

### 3. Real-Time Therapy Sessions

**WebSocket Communication Flow:**
```
User Input → WebSocket → Server
  ↓
Crisis Detection (safety.ts)
  ↓
Persona Context Loading (system prompt + few-shot examples)
  ↓
LLM Processing (Gemini API or Ollama HTTP)
  ↓
Response Generation (persona-appropriate reply)
  ↓
WebSocket → Frontend → UI Display + Speech Synthesis
```

**Session Management:**
- Conversation history maintained per WebSocket connection
- Last 20 turns kept in memory for context
- Session reset capability
- Keep-alive pings every 25 seconds

### 4. LLM Provider System

**Dual Provider Architecture:**
- **Provider Abstraction**: Interface-based design allows runtime switching
- **Lazy Initialization**: Only loads selected provider to reduce startup time
- **Graceful Fallback**: Error handling with user-friendly messages
- **Configuration**: Environment variable-based (`LLM_PROVIDER=gemini|ollama`)

**Gemini (Cloud):**
- Google Gemini 2.5 Flash API
- Higher quality responses
- Requires API key
- Best for: Hackathons, demos, production with internet

**Ollama (Local):**
- Llama 3 model running locally
- Complete privacy (no data leaves machine)
- Zero API costs
- Best for: Privacy-focused deployments, offline operation

### 5. Security & Production Features

**Rate Limiting:**
- 100 requests per 15 minutes per IP address
- Prevents DDoS attacks and API abuse
- Configurable limits per endpoint

**Security Headers (Helmet.js):**
- XSS protection
- CSRF protection
- Clickjacking prevention
- Content Security Policy
- HSTS enforcement

**Input Validation:**
- Email format validation
- Password strength requirements (6-128 characters)
- User type validation
- Input sanitization (XSS prevention)
- SQL injection prevention via parameterized queries

**Structured Logging:**
- JSON-formatted logs with timestamps
- Log levels: info, warn, error
- Request/response tracking
- IP address and user agent logging
- Response time metrics

---

## 🚀 Quick Start

### Prerequisites
- **Node.js 18+** (20+ recommended)
- **npm** or **yarn**
- **For Gemini**: Google Gemini API key ([Get one here](https://makersuite.google.com/app/apikey))
- **For Ollama**: [Install Ollama](https://ollama.com/download) and pull a model

### Option 1: Using Gemini (Cloud) - Recommended for Demos

```bash
# 1. Backend Setup
cd server
echo "GEMINI_API_KEY=your_api_key_here" > .env
echo "LLM_PROVIDER=gemini" >> .env
npm install
npm start

# 2. Frontend Setup (new terminal)
cd web
echo "NEXT_PUBLIC_WS_URL=ws://localhost:8080" > .env.local
echo "NEXT_PUBLIC_API_URL=http://localhost:3001" >> .env.local
npm install
npm run dev

# 3. Open http://localhost:3000
```

### Option 2: Using Ollama (Local) - Privacy-Focused

```bash
# 1. Install and start Ollama
ollama pull llama3
ollama serve

# 2. Backend Setup
cd server
echo "LLM_PROVIDER=ollama" > .env
echo "OLLAMA_MODEL=llama3" >> .env
echo "OLLAMA_BASE_URL=http://localhost:11434" >> .env
npm install
npm start

# 3. Frontend Setup (new terminal)
cd web
echo "NEXT_PUBLIC_WS_URL=ws://localhost:8080" > .env.local
echo "NEXT_PUBLIC_API_URL=http://localhost:3001" >> .env.local
npm install
npm run dev

# 4. Open http://localhost:3000
```

### Environment Variables

**Backend (`server/.env`):**
```env
# LLM Configuration
LLM_PROVIDER=gemini                    # or "ollama"
GEMINI_API_KEY=your_key_here          # Required for Gemini
OLLAMA_MODEL=llama3                    # Required for Ollama
OLLAMA_BASE_URL=http://localhost:11434 # Required for Ollama

# Server Configuration
PORT=8080                               # WebSocket port
API_PORT=3001                          # REST API port
```

**Frontend (`web/.env.local`):**
```env
NEXT_PUBLIC_WS_URL=ws://localhost:8080
NEXT_PUBLIC_API_URL=http://localhost:3001
```

---

## 📊 Key Features

### 🎯 Core Functionality
- **Real-Time Therapy Sessions**: WebSocket-based chat with AI personas
- **Multiple AI Personas**: Pre-built and custom personas with unique personalities
- **Document-to-Persona**: Upload therapy cases to generate AI personas automatically
- **Crisis Detection**: Automatic keyword monitoring with safety responses
- **Session Analytics**: Track progress, duration, and interaction patterns

### 🔒 Security & Production
- **SQLite Persistence**: ACID-compliant database with zero data loss
- **Rate Limiting**: DDoS protection with configurable limits
- **Security Headers**: Helmet.js for XSS, CSRF, and clickjacking protection
- **Input Validation**: Comprehensive sanitization and validation
- **Structured Logging**: Production-ready logging with levels and metrics

### 🧠 AI & ML
- **Dual LLM Support**: Seamless switching between cloud and local models
- **Persona Generation**: AI-powered extraction from therapy documents
- **Few-Shot Learning**: Context-aware responses with example-based learning
- **Conversation Memory**: Maintains context across 20 conversation turns

### 🎨 User Experience
- **Responsive Design**: Tailwind CSS with mobile-first approach
- **Speech Synthesis**: Browser-based text-to-speech for accessibility
- **Real-Time Updates**: Instant message delivery via WebSocket
- **Error Handling**: User-friendly error messages with graceful degradation

---

## 🏆 Technical Highlights

### Architecture Decisions

1. **Provider Pattern for LLMs**: Abstracted interface allows adding new LLM providers without code changes
2. **Service Layer Abstraction**: Auth service interface with multiple implementations (SQLite, GCS, In-Memory)
3. **Middleware-Based Validation**: Reusable validation middleware for all endpoints
4. **Session-Based State**: WebSocket sessions maintain conversation history per connection
5. **Graceful Fallbacks**: Multiple fallback chains ensure system reliability

### Performance Optimizations

- **Lazy LLM Initialization**: Only loads selected provider
- **Conversation History Trimming**: Keeps last 20 turns to manage memory
- **Database Indexing**: Email indexes for fast user lookups
- **Connection Pooling**: Efficient WebSocket connection management
- **Rate Limiting**: Prevents resource exhaustion

### Code Quality

- **Full TypeScript Coverage**: Type safety across frontend and backend
- **Modular Architecture**: Separation of concerns with clear interfaces
- **Error Handling**: Comprehensive try-catch blocks with user-friendly messages
- **Code Documentation**: Inline comments and clear function names
- **Environment-Based Config**: Secure configuration management

---

## 📁 Project Structure

```
TherapyAISunHacks/
├── server/                          # Backend server
│   ├── index.ts                     # Main server (Express + WebSocket)
│   ├── llm.ts                       # LLM provider router
│   ├── safety.ts                    # Crisis detection system
│   ├── database/                    # SQLite database files
│   │   └── users.db                 # User data (gitignored)
│   ├── routes/
│   │   ├── auth.ts                  # Authentication endpoints
│   │   └── personas.ts              # Persona CRUD operations
│   ├── services/
│   │   ├── sqlite-auth.ts          # Production auth service
│   │   ├── fallback-auth.ts         # In-memory fallback
│   │   ├── gcs-service.ts          # Google Cloud Storage auth
│   │   ├── persona-generator.ts    # AI persona generation
│   │   ├── document-parser.ts      # PDF/DOCX parsing
│   │   ├── ollama-llm.ts           # Ollama integration
│   │   └── auth-interface.ts       # Auth service interface
│   ├── middleware/
│   │   ├── validation.ts           # Input validation
│   │   └── logger.ts                # Structured logging
│   ├── knowledge-base/
│   │   ├── personas/                # Default personas
│   │   ├── custom-personas/         # User-generated personas
│   │   └── services/
│   │       └── persona-loader.ts    # Persona loading logic
│   └── package.json                 # Dependencies
│
├── web/                              # Frontend application
│   ├── app/
│   │   ├── page.tsx                 # Landing page
│   │   ├── layout.tsx               # Root layout
│   │   └── globals.css              # Global styles
│   ├── components/
│   │   ├── TherapyAi.tsx           # Main therapy interface
│   │   ├── PractitionerDashboard.tsx
│   │   ├── StudentDashboard.tsx
│   │   ├── PersonaManagement.tsx
│   │   └── PersonaUploadModal.tsx
│   └── package.json                 # Dependencies
│
├── docker-compose.yml                # Docker orchestration
├── Dockerfile                        # Docker image
├── vercel.json                      # Vercel deployment
└── README.md                        # This file
```

---

## 🔧 Customization

### Switching LLM Providers

```bash
# Use Ollama
export LLM_PROVIDER=ollama
export OLLAMA_MODEL=llama3

# Use Gemini
export LLM_PROVIDER=gemini
export GEMINI_API_KEY=your_key
```

### Adjusting LLM Parameters

**Ollama** (`server/services/ollama-llm.ts`):
- `temperature`: 0.3-0.8 (creativity)
- `num_predict`: 200-500 (response length)
- `repeat_penalty`: 1.0-1.2 (repetition control)

**Gemini** (`server/llm.ts`):
- `temperature`: 0.7-0.9 (creativity)
- `maxOutputTokens`: 512-2048 (response length)

---

## 🐛 Troubleshooting

**Connection Issues:**
- Verify WebSocket URL in `web/.env.local`
- Check backend is running on correct ports
- Ensure firewall allows connections

**LLM Errors:**
- **Gemini**: Verify API key is valid and has quota
- **Ollama**: Ensure service is running (`ollama serve`)
- Check model is installed (`ollama list`)

**Database Issues:**
- SQLite database auto-creates on first run
- Check file permissions in `server/database/`
- Verify database directory exists

---

## ⚠️ Safety & Disclaimer

**This is an educational tool for training purposes only.**

- ❌ **NOT** a substitute for professional mental health services
- ❌ **NOT** a crisis intervention tool
- ✅ **IS** a training platform for students and practitioners

If someone is in immediate danger, contact local emergency services immediately.

---

## 📝 License

This project is open source and available for educational purposes.

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

---

## 📧 Contact

For questions or feedback, please open an issue on GitHub.

---

**Built with ❤️ using Next.js, Express, TypeScript, and modern AI technologies.**
