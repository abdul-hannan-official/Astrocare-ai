# ASTROCARE AI

**Astronaut Health Intelligence and Monitoring System**  
Team **Astrovibes** — NASA Space Apps Challenge 2026

ASTROCARE AI is a full-stack space health command center built with **Vanilla HTML5, CSS3, and JavaScript** on the frontend, **Node.js + Express** on the backend, **SQLite (`better-sqlite3`)** for persistent storage, **Chart.js** for telemetry analytics, and **Lucide** icons.

> **Important Transparency Notice**: All astronaut profiles, vital readings, and demonstration thresholds in this application are **simulated** for hackathon demonstration and testing. ASTROCARE AI is not medically validated flight software and does not diagnose medical conditions.

---

## Features

1. **Mission Dashboard**: Crew profile for fictional astronaut **Alex Morgan** (`ORBIT-04`), Mission Day & Duration progress, 6 vital KPI cards (Heart Rate, SpO2, Blood Pressure, Body Temperature, Sleep Duration, Activity Level), overall monitoring status, and a 24-hour trend chart.
2. **Live Health Monitoring**: Periodic simulated telemetry generator (`6s` interval toggle or single tick), manual vital sign entry form with validation and quick test presets (`Normal`, `Moderate Watch`, `High Alert`), interactive historical Chart.js inspector, and chronological readings log.
3. **Explainable AI Health Risk Engine**: Evaluates readings against configurable demonstration thresholds and recent rolling baseline shifts (`LOW`, `MODERATE`, `HIGH`), showing the exact triggering measurements and non-diagnostic next-step guidance.
4. **Smart Alert Center**: Filterable monitoring warnings (`All`, `Unacknowledged`, `HIGH`, `MODERATE`) with timestamps, reasons, next-step guidance, and persistent `Acknowledge` actions.
5. **AI Health Assistant**: Conversational assistant grounded strictly in stored SQLite telemetry. Uses server-side `@google/genai` (`gemini-4-hydrogen`) when `GEMINI_API_KEY` is configured, with a deterministic reading-grounded fallback so it always works reliably without inventing measurements.
6. **Health Analytics**: 24-hour vital trends, 7-day health history, sleep duration analytics, alert history chart, and downloadable CSV report (`/api/analytics/export.csv`).
7. **NASA Research & Sources**: Direct links to the NASA Open Science Data Repository (`osdr.nasa.gov`), NASA Life Sciences Portal (`nlsp.nasa.gov`), and NASA Human Research Program (`nasa.gov/hrp/hazards/`), paired with spaceflight physiology background.

---

## API Endpoints

- `GET /api/health/current` — Latest reading, astronaut profile, risk analysis, unacknowledged alert count
- `GET /api/health/history` — Stored reading history (`?limit=&hours=`)
- `POST /api/health/readings` — Validate, persist, and evaluate a manual reading
- `POST /api/health/simulate` — Generate and persist one simulated telemetry reading
- `GET /api/alerts` — List monitoring alerts (`?severity=&status=`)
- `POST /api/alerts/:id/acknowledge` — Acknowledge an alert
- `GET /api/thresholds` / `PUT /api/thresholds` / `POST /api/thresholds/reset` — Manage demonstration thresholds
- `GET /api/analytics` — 24h trends, 7-day daily summaries, sleep stats, alert timeline
- `GET /api/analytics/export.csv` — Download stored telemetry as CSV
- `GET /api/assistant/history` & `POST /api/assistant/chat` — Reading-grounded AI Health Assistant

---

## Setup & Run Instructions

1. Copy `.env.example` to `.env` if running locally (optional `GEMINI_API_KEY` enables Gemini-backed assistant phrasing; without it, the deterministic grounded analyzer runs automatically).
2. Install dependencies:
   ```bash
   npm install
   ```
3. Run unit tests for the Risk Engine:
   ```bash
   npm test
   ```
4. Start the development server (port 3000):
   ```bash
   npm run dev
   ```
5. Build for production and start:
   ```bash
   npm run build
   NODE_ENV=production npm start
   ```
