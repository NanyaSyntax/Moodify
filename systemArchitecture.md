# System Architecture — Moodify

This document outlines the technical design and architecture for the Moodify product.  
The system is structured into **three major layers**: Frontend, Backend, and Data Processing Engine.

---

## 🏛️ High-Level Architecture Diagram

User → Frontend (React) → Backend API (Node.js) → Spotify API
↓
Data Processing Engine (Python)
↓
Database (MongoDB)
↓
Frontend UI


---

## 🎨 Frontend (Client Layer)
**Tech Stack:** React / Next.js, TailwindCSS, Chart.js  

**Responsibilities:**
- Handle user login via Spotify OAuth redirect.
- Display dashboards, mood insights, and charts.
- Send requests to backend API for mood + trend data.

**Key UI Pages:**
1. Login / Connect Spotify
2. Dashboard (mood summary)
3. Emotional Timeline Visualization
4. Song Insight View

---

## 🔗 Backend (Application Layer)
**Tech Stack:** Node.js + Express  

**Responsibilities:**
- Manage Spotify OAuth authentication flow.
- Fetch user listening history from Spotify APIs.
- Store processed results in the database.
- Expose REST endpoints to frontend.

**API Endpoints Example:**
| Endpoint | Description |
|---------|-------------|
| `GET /auth/login` | Initiates Spotify login |
| `GET /user/history` | Retrieves user listening data |
| `GET /mood/summary` | Returns processed emotional profile |
| `GET /mood/timeline` | Returns trends for visualization |

---

## 🧠 Data Processing Engine (Insight Layer)
**Tech Stack:** Python  

**Tasks:**
- Analyze song tempo/BPM for energy score.
- Perform lyric sentiment analysis (NLP).
- Detect mood shifts based on repeat & skip patterns.
- Map data to psychology scoring model (Big Five traits).

**Output Example:**
```json
{
  "mood": "Calm",
  "energy": 0.62,
  "emotional_stability": 0.78
}


🗄️ Database Layer

Preferred: MongoDB (flexible user emotion profiles)

Collections:

users

listening_history

emotion_profiles

trend_snapshots


✅ Feasibility Justification

Spotify Web API supports listening data requests and OAuth access.

NLP and music tempo classification are well-documented and stable technologies.

React + Chart.js allows smooth mood visualization.

Architecture is scalable and supports future AI recommendation features.


---

# Repository Structure

moodify/
│ README.md
│ systemArchitecture.md
│ .gitignore
│ package.json
│ src/
├── frontend/
├── backend/
└── processing/