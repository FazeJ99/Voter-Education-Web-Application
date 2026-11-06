# VoterEdu Kenya 🇰🇪

> **Vote based on facts, not noise.** An independent, transparent, and verified civic education platform empowering Kenyan citizens ahead of the 2027 General Elections.

![VoterEdu Demo](assets/voteredu-demo.gif)

---
## 📌 Overview

During election cycles, public discourse often becomes cluttered with viral misinformation, rhetoric, and polarized debates. **VoterEdu** is engineered to eliminate voter confusion by providing a single, reliable hub for electoral transparency. 

Built as a responsive web application backed by resilient APIs, VoterEdu allows Kenyan voters to examine candidates' concrete track records, scrutinize policy manifestos against key socio-economic pillars, read verified peer reviews, track civic events, and plan their travel logistics to polling stations seamlessly.

---

## 🗳️ Impact on the 2027 General Elections

- **Combating Misinformation & Polarized Echo Chambers:** Delivers structured, sourced manifesto stances across critical public interest issues (fiscal policy, governance, agriculture, and cost of living) rather than viral soundbites.
- **Accountability & Public Scorecards:** Features voter review logs with interactive rating matrices, enabling communities to leave qualitative reviews and score candidates on integrity, performance, and transparency.
- **Logistical Accessibility & Turnout Enhancement:** Integrates with local transit estimates, ensuring voters can budget and map routes to polling centers to reduce election-day absenteeism.
- **Civic Mobilization:** Aggregates verified town halls, policy addresses, and campaign rallies so voters can engage candidates directly across key venues.

---

## ✨ Key Features

- **Candidate Profiles & Manifesto Matrix:** Comprehensive profiles containing candidate bios, coalition affiliations, verified badges, and structured breakdowns across key pillars:
  - *Experience & Track Record*
  - *Core Vision Statement*
  - *Taxation & Fiscal Policy*
  - *Agriculture & Food Security*
  - *Governance & Devolution*
  - *Cost of Living Mitigation*
- **Candidate Review Logs & Trust Scoring:** Interactive review logging enabling verified citizens to submit structured ratings (1–5 stars) and critical verdicts.
- **Side-by-Side Candidate Comparison:** Matrix view to evaluate two or more candidates head-to-head on key election themes.
- **Polling Station Locator & Ride Fare Estimator:** Integrated route planner connecting local landmarks with polling stations, calculating travel time (ETA) and estimated fares (Boda, Standard, XL) across multiple providers.
- **Upcoming Civic Events & Rallies Feed:** Real-time stream of county town halls, presidential debates, and public interest dialogues with venue, time, and expected crowd capacity details.
- **Resilient & Observable Architecture:** Built with partner API resilience (exponential backoff, in-memory graceful fallbacks, and stale-data indicators) alongside low-overhead request monitoring and health metrics.

---

## 🛠️ Architecture & Tech Stack

- **Frontend:** React.js, React-Bootstrap, React Router, HTML5/CSS3
- **Backend / API Proxy:** Node.js, Express.js
- **Database / Cache:** SQLite (`better-sqlite3`), In-Memory Resilience Fallback Cache
- **Security & Resilience:** 
  - Token-safe API Key Authentication (`X-API-Key` with SHA-256 fingerprinting)
  - In-memory rate limiting with `Retry-After` headers
  - Resilient HTTP client wrapper (`resilientFetch`) featuring timeout safeguards (1.5s) and exponential backoff retry logic
- **Observability:** Custom lightweight performance monitoring middleware with a protected `/stats` metrics endpoint

---

## 🚀 Getting Started

### Prerequisites

- Node.js (v18.0.0 or higher)
- npm or yarn

### 1. Clone the Repository

```bash
git clone https://github.com/FazeJ99/Voter-Education-Web-Application.git
cd Voter-Education-Web-Application/voter.fs
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Environment Variables Configuration

Create a `.env` file in the root backend directory:

```env
PORT=5000
API_KEYS=<your-internal-client-key>,<partner-consumer-key>
MY_API_KEY=<your-primary-key>
PARTNER_URL=https://demand-flat-says-protocol.trycloudflare.com
PARTNER_API_KEY=<upstream-partner-key>
```

### 4. Running the Application

In separate terminal windows:

**Start the Express API server:**
```bash
node db/server.js
```

**Start the React frontend application:**
```bash
npm start
```

Access the user interface at `http://localhost:3000`.

---

## 📊 Monitoring & Observability (`/stats`)

The backend exposes a runtime health and metrics endpoint protected by API authentication:

* **Endpoint:** `GET /stats`
* **Headers:** `X-API-Key: <your-api-key>`

### Example Response:

```json
{
  "startedAt": "2026-11-06T10:22:46.926Z",
  "uptimeSeconds": 120,
  "total": 60,
  "clientErrors": 29,
  "serverErrors": 0,
  "errorRatePercent": 0,
  "avgMs": 1.3,
  "routes": {
    "GET /api/candidates": {
      "count": 16,
      "clientErrors": 0,
      "serverErrors": 0,
      "avgMs": 1.6,
      "maxMs": 2.3
    },
    "GET /api/candidates/:candidateId": {
      "count": 13,
      "clientErrors": 4,
      "serverErrors": 0,
      "avgMs": 1.8,
      "maxMs": 3.8
    },
    "GET /api/rallies": {
      "count": 6,
      "clientErrors": 0,
      "serverErrors": 0,
      "avgMs": 1.1,
      "maxMs": 1.5
    }
  }
}
```

---

## 📄 License & Attribution

This project is developed for educational and civic transparency purposes.