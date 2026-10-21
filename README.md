# MEGA MX 🎓

> **Turn long, disorganized course syllabi into clean, interactive, mobile-friendly academic roadmaps.**

[![Hacktoberfest 2026](https://img.shields.io/badge/Hacktoberfest-2026-ff7a00?style=for-the-badge&logo=hacktoberfest&logoColor=white)](https://hacktoberfest.com/)
[![Track](https://img.shields.io/badge/Category-No--Code%20%2F%20Low--Code-indigo?style=for-the-badge)](https://hacktoberfest.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-emerald.svg?style=for-the-badge)](LICENSE)
[![React](https://img.shields.io/badge/React-18-61DAFB?style=for-the-badge&logo=react&logoColor=black)](https://react.dev/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?style=for-the-badge&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![Vite](https://img.shields.io/badge/Vite-5-646CFF?style=for-the-badge&logo=vite&logoColor=white)](https://vitejs.dev/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.4-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)
[![Node.js](https://img.shields.io/badge/Node.js-20+-339933?style=for-the-badge&logo=node.js&logoColor=white)](https://nodejs.org/)

---

## 📌 Problem & Motivation

University syllabi are notorious for being 10-to-20 page dense PDFs filled with administrative boilerplate. Critical assignment deadlines, examination windows, and grade weighting calculations are often buried across pages of fine print. Students frequently miss early homework due dates or fail to recognize which components carry the highest academic weight.

**SyllabusX** bridges this gap. By leveraging the **Gamma REST API** and a structured pedagogical prompt engine, SyllabusX transforms messy syllabus text into a **clean, mobile-first academic roadmap**. Students immediately see their semester broken down into four chronological phases, track milestones with clear dates, and execute a custom **"How to Ace This Class"** strategy derived mathematically from their professor's grading rubric.

---

## ✨ Key Features

- 📱 **Mobile-First Responsive Design**: Optimized for instant reading on smartphones and laptops alike—no horizontal scrolling or text walls.
- ⏱️ **Four-Part Chronological Phases**:
  1. **Phase 1: Getting Started** (Expectations, materials, early onboarding)
  2. **Phase 2: Building Foundations** (Core principles, problem sets, cadence)
  3. **Phase 3: Mid-Semester Progress** (Intermediate topics, midterms, projects)
  4. **Phase 4: Final Preparation & Completion** (Final project freeze, exam prep, course wrap-up)
- 🎯 **Visual Milestone Cards**: Clearly separates confirmed exam dates from suggested planning windows. Never invents dates or deadlines.
- 🏆 **"How to Ace This Class" Checklist**: Mathematically highlights which grade categories carry the greatest impact and provides targeted action strategies.
- ⚡ **Asynchronous Gamma REST API Integration**: Communicates directly with Gamma's Agent API (`POST /v1.0/agent/generations`, `format: "webpage"`) using secure status polling.
- 🧪 **Offline Mock Generation Service**: Out-of-the-box local development mode for contributors who don't have paid Gamma API credentials.
- 🔒 **Zero Storage & Privacy First**: No accounts, logins, or tracking required. Syllabus inputs are processed in-memory and never permanently stored.
- 🚀 **1-Click Sample Pre-fills**: Instant test buttons for Computer Science and Biology syllabi so evaluators and contributors can test the workflow in seconds.

---

## 🛠️ Architecture & Workflow

```
                                  USER JOURNEY
                                        │
                      1. Open SyllabusX Landing Page
                                        │
                      2. Click "Create My Roadmap"
                                        │
                      3. Fill in 4 Course Fields:
                         - Course Name
                         - Instructor Name
                         - Grading Breakdown
                         - Critical Deadlines
                                        │
                      4. Submit Form (Client Validation)
                                        │
                                        ▼
                   ┌─────────────────────────────────────────┐
                   │            BACKEND API SERVER           │
                   │        POST /api/generate (100kb limit) │
                   └────────────────────┬────────────────────┘
                                        │
                         Is GAMMA_API_KEY Configured?
                                        │
                      ┌─────────────────┴─────────────────┐
                      │ YES                               │ NO / MOCK_MODE=true
                      ▼                                   ▼
          ┌───────────────────────────┐      ┌───────────────────────────┐
          │      Gamma REST API       │      │   Mock Generation Engine  │
          │ POST /agent/generations   │      │ Simulates progress & rich │
          │ format: "webpage"         │      │ interactive roadmap       │
          └─────────────┬─────────────┘      └─────────────┬─────────────┘
                        │                                  │
                        ▼                                  ▼
           Poll GET /agent/generations/:id    Poll GET /api/generation-status/:id
           (Every 3s, timeout 120s)           (Every 3s)
                        │                                  │
                        └─────────────────┬────────────────┘
                                          │
                                          ▼
                         Frontend displays finished roadmap:
                         - Embedded Webpage View
                         - "Open in New Tab" Link
                         - Interactive Task Checklist
```

---

## 🚀 Quickstart & Local Setup

### 1. Prerequisites

- [Node.js](https://nodejs.org/) v18+ or v20+
- [Git](https://git-scm.com/)

### 2. Clone the Repository

```bash
git clone https://github.com/example/syllabusx.git
cd syllabusx
```

### 3. Backend Setup

```bash
cd backend
npm install
cp .env.example .env
```

#### Environment Variables (`backend/.env`)

```ini
# Server Port
PORT=4000

# Gamma REST API Key (optional - leave empty for Mock Mode)
GAMMA_API_KEY=

# Gamma Base URL
GAMMA_API_BASE_URL=https://public-api.gamma.app/v1.0

# Polling Interval (in ms)
GAMMA_POLL_INTERVAL_MS=3000

# Polling Timeout (in ms)
GAMMA_POLL_TIMEOUT_MS=120000

# Mock Mode (automatically true if GAMMA_API_KEY is unset)
MOCK_MODE=false

# Allowed Frontend Origin for CORS
CORS_ORIGIN=http://localhost:5173
```

Start the backend server:

```bash
npm run dev
# Running on http://localhost:4000
```

### 4. Frontend Setup

In a new terminal:

```bash
cd frontend
npm install
npm run dev
# Running on http://localhost:5173
```

Visit **[http://localhost:5173](http://localhost:5173)** in your browser!

---

## 🧪 Testing

SyllabusX includes a test suite covering form validation, prompt generation, Gamma API communication, status polling, and server endpoints.

```bash
# Run backend tests
cd backend
npm test
```

Test coverage includes:
- ✅ Missing or malformed course input validation
- ✅ Whitespace sanitization & character boundary checks
- ✅ Strict prompt compliance (4 phases, milestone cards, "How to Ace This Class")
- ✅ URL validation for external Gamma links
- ✅ Mock mode generation lifecycle & error recovery
- ✅ Asynchronous endpoint testing via Node.js native test runner

---

## 📖 Gamma REST API Integration Details

Gamma provides an asynchronous generative AI agent API:

1. **Trigger Generation**:
   `POST https://public-api.gamma.app/v1.0/agent/generations`
   - Header: `X-API-KEY: sk-gamma-...`
   - Body: `{ "prompt": "...", "format": "webpage" }`
   - Returns: `{ "generationId": "gen_...", "status": "pending" }`

2. **Poll Status**:
   `GET https://public-api.gamma.app/v1.0/agent/generations/{generationId}`
   - Header: `X-API-KEY: sk-gamma-...`
   - Statuses: `"pending"` ➔ `"completed"` (with `gammaUrl`) or `"failed"`.

3. **Fallback & Mock Mode**:
   When no key is configured, SyllabusX runs in separated Mock Mode. Mock generations return `isMock: true` and display a rich interactive roadmap matching Gamma's structure.

Detailed documentation is available in [docs/GAMMA_INTEGRATION.md](docs/GAMMA_INTEGRATION.md) and [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md).

---

## 🤝 Contributing to Hacktoberfest

We welcome all contributions! Whether you're adding university syllabus templates, improving mobile accessibility, adding export features, or fixing typos, check out our [CONTRIBUTING.md](CONTRIBUTING.md) guide.

### Contribution Ideas
- [ ] Export milestone deadlines to `.ics` calendar format
- [ ] Dark mode toggle
- [ ] Syllabus file upload parser (.pdf/.docx text extraction)
- [ ] Multi-language translation support

---

## 📄 License

This project is licensed under the [MIT License](LICENSE) — free and open for students and universities worldwide.
