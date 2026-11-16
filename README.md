# 🌊 FloodLens AI
### AI-Based Flood Prediction & Risk Mapping System

<p align="center">
  <strong>Smart Flood Monitoring • Risk Assessment • Early Warning • Disaster Awareness</strong>
</p>

<p align="center">
  <a href="https://flood-lens-ai-gamma.vercel.app/">🌐 Live Website</a> •
  <a href="https://github.com/shrutisingh3029/FLOODLENS-AI">💻 GitHub Repository</a> •
  <a href="https://github.com/shrutisingh3029/FLOODLENS-AI/issues">🐛 Report an Issue</a>
</p>

---

## 📌 About the Project

**FloodLens AI** is an AI-based flood prediction and risk mapping project developed by **Team SOLVIX, MIT ADT University**.

The platform aims to support flood preparedness and disaster awareness by bringing flood-risk assessment, interactive maps, weather information, citizen reporting, and safety assistance together in one web application.

The project demonstrates how technology, environmental data, and digital mapping can help users understand potential flood risks and access useful preparedness information.

> ⚠️ **Disclaimer:** FloodLens AI is an academic demonstration project. Its sample predictions and alerts are not official government warnings. Always follow instructions from local disaster-management authorities.

---

## 🌐 Live Project

| Resource | Link |
|---|---|
| Live Website | [Open FloodLens AI](https://flood-lens-ai-gamma.vercel.app/) |
| GitHub Repository | [FLOODLENS-AI](https://github.com/shrutisingh3029/FLOODLENS-AI) |
| Source Code | [Browse Project Files](https://github.com/shrutisingh3029/FLOODLENS-AI/tree/main) |
| Issues & Feedback | [Report an Issue](https://github.com/shrutisingh3029/FLOODLENS-AI/issues) |

---

## ✨ Key Features

### 1. 🌧️ Flood Risk Assessment
- Evaluate flood-risk levels using environmental parameters.
- Display risk scores and assessment results.
- Explore factors that may influence flood conditions.

### 2. 🗺️ Interactive Flood Map
- Explore map-based flood-risk information.
- View demonstration flood-risk locations.
- Understand geographical risk distribution.

### 3. 🌦️ Weather Forecast
- Access weather forecast information.
- Retrieve forecast data using the Open-Meteo API.
- Explore weather conditions relevant to flood awareness.

### 4. 🛣️ Route & Shelter Finder
- Explore route estimates.
- Find mapped shelter locations.
- Use public mapping services for geographical information.

### 5. 📢 Citizen Flood Reporting
- Submit flood observations through the platform.
- User authentication through Supabase.
- Store citizen reports using Supabase PostgreSQL and Row Level Security.

### 6. 🔔 Notification Centre
- View flood-related notifications.
- Explore sample alerts based on different risk levels.

### 7. 📊 Historical Flood Analysis
- Explore sample flood-related location records.
- Compare demonstration risk information.

### 8. 🤖 AI Safety Assistant
- Interactive safety assistance interface.
- Backend-powered responses using the Gemini API when configured.
- Provides general flood preparedness guidance.

---

## 🛠️ Technology Stack

| Category | Technologies |
|---|---|
| Frontend | HTML, CSS, JavaScript |
| Frontend Tooling | Vite, React, TypeScript |
| Backend | Python, Flask |
| Database | Supabase PostgreSQL |
| Authentication | Supabase Auth |
| AI Integration | Gemini API |
| Mapping | Leaflet, OpenStreetMap |
| Weather API | Open-Meteo |
| Routing | OSRM |
| Deployment | Vercel, Python-compatible hosting |

### Useful Technology Links
- [React](https://react.dev/)
- [Vite](https://vite.dev/)
- [TypeScript](https://www.typescriptlang.org/)
- [Flask](https://flask.palletsprojects.com/)
- [Supabase](https://supabase.com/)
- [Google Gemini](https://ai.google.dev/)
- [Leaflet](https://leafletjs.com/)
- [OpenStreetMap](https://www.openstreetmap.org/)
- [Open-Meteo](https://open-meteo.com/)

---

## 📂 Project Structure

```text
FLOODLENS-AI/
│
├── .github/
│   └── workflows/
│
├── public/
│   ├── auth.js
│   ├── auth-config.js
│   ├── backend-config.js
│   ├── features.js
│   └── features.css
│
├── src/
│   ├── App.tsx
│   ├── index.css
│   └── main.tsx
│
├── SOLVIX_Flood_Prediction/
│   ├── app.py
│   ├── requirements.txt
│   ├── data/
│   ├── static/
│   └── templates/
│
├── supabase/
│   └── migrations/
│       └── 20261116_citizen_reports.sql
│
├── index.html
├── features.js
├── features.css
├── package.json
├── vite.config.ts
├── DEPLOYMENT.md
└── README.md
