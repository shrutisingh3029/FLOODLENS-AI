# FloodLens AI
### AI-Based Flood Prediction & Risk Mapping System

FloodLens AI is an academic disaster-awareness project by **Team SOLVIX** that brings flood-risk assessment, map-based exploration, weather information, route and shelter lookup, and community flood reporting into one web experience.

The project is intended to demonstrate how digital tools can support flood preparedness and situational awareness. It is **not an official warning system** and must not replace instructions from disaster-management authorities or emergency services.

---

## Table of Contents
- [Project Overview](#project-overview)
- [Key Features](#key-features)
- [Technology Stack](#technology-stack)
- [Repository Structure](#repository-structure)
- [Getting Started](#getting-started)
- [Configuration](#configuration)
- [Database Setup](#database-setup)
- [Backend Deployment](#backend-deployment)
- [Data Sources and Limitations](#data-sources-and-limitations)
- [Validation](#validation)
- [Team](#team)

## Project Overview

FloodLens AI combines a flood-risk assessment interface with supporting tools for exploring weather conditions, viewing map information, finding routes and mapped shelters, and submitting citizen observations. Authentication is provided through Supabase Auth, while the Flask API supports authenticated reporting and the assistant endpoint.

The project contains a Vite-based frontend and a Python/Flask backend in a separate directory. The frontend can be run locally without deploying the backend; backend-dependent capabilities require the API to be configured and available.

## Key Features

| Feature | What it does |
|---|---|
| Flood Risk Assessment | Evaluates submitted environmental parameters using the project's current assessment logic. |
| Interactive Flood Map | Displays map information and demonstration risk locations. |
| Weather Forecast | Retrieves forecast information through Open-Meteo. |
| Route & Shelter Finder | Provides route estimates and mapped shelter lookups using public mapping services. |
| Citizen Flood Reporting | Allows signed-in users to submit flood observations. |
| Authentication | Supports Supabase email/password authentication and user sessions. |
| Notification Centre | Displays sample flood alerts and notification interactions. |
| Historical Flood Analysis | Presents comparison views based on the project's sample location records. |
| Safety Assistant | Provides safety guidance; model-powered replies require the configured Gemini backend. |

## Technology Stack

**Frontend**
- HTML, CSS and JavaScript
- Vite and the React/TypeScript toolchain included in the project
- Supabase JavaScript client
- Leaflet and public map services

**Backend and data**
- Python and Flask
- Supabase Auth for user authentication and access-token validation
- Supabase Postgres with Row Level Security (RLS) for citizen reports
- Gemini API for model-powered assistant responses (optional; requires a server-side API key)

**Deployment**
- Vercel for the frontend
- A Python-compatible host for the Flask API (for example, Render or another persistent service)

## Repository Structure

```text
.
├── index.html                         # Main FloodLens web interface
├── features.js / features.css         # Interactive feature behaviour and styling
├── backend-config.js                  # Frontend API-origin configuration
├── public/
│   ├── auth.js                        # Supabase authentication interface
│   ├── auth-config.js                 # Public Supabase browser configuration
│   ├── backend-config.js              # Public API-origin configuration
│   └── features.js / features.css     # Static frontend feature assets
├── src/                               # Vite React/TypeScript source
├── SOLVIX_Flood_Prediction/
│   ├── app.py                         # Flask API
│   ├── requirements.txt               # Python dependencies
│   ├── data/                          # Project data files
│   ├── static/                        # Flask app static assets
│   └── templates/                     # Flask app templates
├── supabase/
│   └── migrations/
│       └── 20261116_citizen_reports.sql
├── .github/workflows/                 # Automated validation workflow
├── DEPLOYMENT.md                      # Additional deployment instructions
├── package.json
└── vite.config.ts
```

## Getting Started

### Prerequisites

- Node.js and npm
- Python 3.10 or later recommended for the Flask backend
- A Supabase project for authentication and persistent citizen reports
- A Gemini API key only if model-powered assistant responses are required

### 1. Clone the repository

```bash
git clone https://github.com/shrutisingh3029/FLOODLENS-AI.git
cd FLOODLENS-AI
```

### 2. Run the frontend

```bash
npm install
npm run dev
```

Vite prints a local development URL in the terminal (normally `http://localhost:5173`). Open that URL in your browser.

To create a production build:

```bash
npm run build
npm run preview
```

### 3. Run the Flask backend (optional)

Open a second terminal:

```bash
cd SOLVIX_Flood_Prediction
python -m venv .venv
```

Activate the environment:

**Windows PowerShell**
```powershell
.venv\Scripts\Activate.ps1
```

**macOS / Linux**
```bash
source .venv/bin/activate
```

Install dependencies and start the API:

```bash
pip install -r requirements.txt
python app.py
```

For production hosting, use the host's configured start command (the deployment notes use `gunicorn app:app`). Configure the environment variables described below on the backend host.

## Configuration

### Frontend configuration

Check these files before deploying:

- `public/auth-config.js`: Supabase project URL and browser **publishable** key.
- `public/backend-config.js`: deployed Flask API base URL.
- `backend-config.js`: root-level API configuration used by the project deployment setup.

The Supabase publishable key is designed for browser use. **Never put a Supabase service-role key, secret key, Gemini API key, or other private credential in frontend code.**

If you fork or deploy this project under a different Supabase project or API host, update the configuration to match your own services.

### Backend environment variables

Configure these in the backend hosting provider's environment settings:

| Variable | Purpose |
|---|---|
| `GEMINI_API_KEY` | Server-side Gemini API key for model-powered assistant responses. |
| `GEMINI_MODEL` | Optional model name; the application configuration provides a default. |
| `FRONTEND_ORIGINS` | Comma-separated frontend origins allowed to call the API. |
| `SUPABASE_URL` | Supabase project URL used for token validation and database access. |
| `SUPABASE_PUBLISHABLE_KEY` | Matching Supabase publishable key used by the backend integration. |
| `FLOODLENS_DB_PATH` | Optional path for the SQLite/demo report store where applicable. |

A placeholder file is provided at `SOLVIX_Flood_Prediction/.env.example`. Do not commit real credentials.

## Database Setup

Persistent citizen reports use Supabase Postgres. The SQL schema and Row Level Security policies are defined in:

`supabase/migrations/20261116_citizen_reports.sql`

To set up the table in your Supabase project:

1. Open the Supabase Dashboard for your project.
2. Go to **SQL Editor** and create a new query.
3. Copy the contents of the migration file into the editor and run it once.
4. Confirm that the `citizen_reports` table and its RLS policies have been created.
5. Configure the matching `SUPABASE_URL` and `SUPABASE_PUBLISHABLE_KEY` values on the backend host.

The API validates the signed-in user's Supabase access token. RLS policies restrict report access to rows belonging to the authenticated user. Do not disable RLS to make the application work.

## Backend Deployment

The Flask service is located in `SOLVIX_Flood_Prediction`.

Typical deployment settings:

- **Root directory:** `SOLVIX_Flood_Prediction`
- **Install command:** `pip install -r requirements.txt`
- **Start command:** `gunicorn app:app`

After deployment:

1. Add the required environment variables in the hosting dashboard.
2. Set the frontend API base URL in `public/backend-config.js` to the deployed backend origin.
3. Add the deployed frontend URL(s) to `FRONTEND_ORIGINS`.
4. Add the frontend production and preview URLs to Supabase Authentication's allowed redirect URLs.
5. Redeploy the frontend and test sign-in, report submission, and API-backed assistant functionality.

More detailed notes are available in [DEPLOYMENT.md](./DEPLOYMENT.md).

## Data Sources and Limitations

Please read these limitations before using or demonstrating the application:

- **Risk assessment:** The current assessment logic is a project demonstration. Do not interpret its output as a validated operational flood forecast.
- **Weather:** Forecast information is retrieved from Open-Meteo. Availability and coverage depend on that public service.
- **Maps and routes:** Route estimates use OSRM; mapped shelter lookups use OpenStreetMap/Overpass. Routes are not flood-aware, and shelter listings or availability are not independently verified.
- **Citizen reports:** User submissions are observations, not verified incidents. They are not automatically forwarded to emergency services.
- **Notifications:** The Notification Centre includes simulated/sample alerts; they are not official government warnings.
- **Historical analysis:** Current comparison views use sample location records, not a verified historical time series.
- **Assistant:** Model-powered responses depend on a correctly configured backend and Gemini API key. Guidance should not replace local emergency instructions.
- **Availability and persistence:** Production reliability depends on the selected hosting, database, and external service availability. Configure persistent storage and backups where required.

In an emergency, follow instructions from local authorities and contact the appropriate emergency services.

## Validation

The repository includes a GitHub Actions workflow for project checks. The documented checks include:

- JavaScript syntax validation for the feature script
- Frontend production build using `npm run build`
- Python syntax compilation for the Flask application

A successful build does not by itself verify live API integrations, database policies, authentication redirects, or real-world flood-data accuracy. Test those separately in the deployed environment.

## Team

**Team SOLVIX**  
MIT ADT University

---

## Contributing

For project improvements, create a branch, make focused changes, run the relevant checks, and open a pull request with a clear description of the change and how it was tested.

## License

No license has been specified in this repository yet. Contact the project maintainers before reusing, distributing, or adapting the project.
