# Contributing to SyllabusX

Thank you for your interest in contributing to **SyllabusX**! SyllabusX is an open-source academic productivity web application participating in **Hacktoberfest 2026** under the **No-Code / Low-Code** category.

We welcome all contributions from students, educators, and developers worldwide: from beginner-friendly documentation improvements to core feature implementations and syllabus parsers.

---

## Code of Conduct

We are committed to providing a welcoming, inclusive, and harassment-free experience for everyone. Please be respectful, constructive, and kind in all discussions, pull requests, and issues.

---

## How to Get Involved in Hacktoberfest

1. **Find an Issue**: Browse open issues tagged with `good first issue` or `hacktoberfest`.
2. **Comment**: Leave a comment indicating you would like to work on it.
3. **Fork & Branch**: Create a feature branch with a descriptive name (e.g., `feat/dark-mode`, `fix/form-validation`).
4. **Develop & Test**: Implement your changes and verify all tests pass locally.
5. **Open a PR**: Submit your pull request with a clear description referencing the issue.

---

## Local Development Setup

### Prerequisites

- **Node.js**: v18.0.0 or higher (v20+ recommended)
- **npm**: v9+ or higher
- **Git**

### Installation Steps

1. Clone your fork of the repository:
   ```bash
   git clone https://github.com/<your-username>/syllabusx.git
   cd syllabusx
   ```

2. Install backend dependencies:
   ```bash
   cd backend
   npm install
   ```

3. Configure your backend environment:
   ```bash
   cp .env.example .env
   ```
   *Note: If you do not have a `GAMMA_API_KEY`, leave it blank. The app will automatically run in **Mock Mode**, providing a full local development experience without paid credentials.*

4. Install frontend dependencies:
   ```bash
   cd ../frontend
   npm install
   ```

---

## Running the Application Locally

In two separate terminal windows:

### Terminal 1: Backend Server
```bash
cd backend
npm run dev
# Starts backend at http://localhost:4000
```

### Terminal 2: Frontend Client
```bash
cd frontend
npm run dev
# Starts Vite dev server at http://localhost:5173
```

Open [http://localhost:5173](http://localhost:5173) in your browser.

---

## Running Tests

Before submitting a Pull Request, verify that all backend tests and frontend builds pass cleanly:

### Backend Tests
```bash
cd backend
npx tsc
npm test
```

### Frontend Build & Lint Check
```bash
cd frontend
npm run build
```

---

## Beginner-Friendly Contribution Ideas

- **Syllabus Presets**: Add realistic syllabus presets for Humanities, Engineering, Medicine, or Business in `backend/src/server.ts`.
- **UI Themes**: Add dark mode / high-contrast academic themes in Tailwind.
- **Export Formats**: Add iCalendar (.ics) or Google Calendar deadline export options.
- **Localization**: Translate the interface into Spanish, French, German, Mandarin, or Hindi.
- **Rubric Visualizer**: Enhance the "How to Ace This Class" section with interactive grade-weight sliders.

---

## Pull Request Guidelines

- Keep pull requests focused on a single feature or bug fix.
- Follow existing code formatting and naming conventions.
- Ensure all tests pass.
- Link relevant issues using `Fixes #<issue-number>` or `Closes #<issue-number>`.
- Add screenshot or GIF demonstration for frontend UI changes.
