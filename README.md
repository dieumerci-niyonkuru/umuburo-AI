# Umuburo AI

Umuburo AI is a malaria early-warning prototype for Rwanda. It combines surveillance, climate, and prevention indicators to show explainable risk forecasts for district teams. Its demo data is illustrative and is not official RBC data.

## Repository layout

- `web/` — Next.js web application (recommended Railway deployment)
- `backend/` — FastAPI API service and its JSON data
- `dashboard/` — standalone offline demo dashboard
- `data/`, `model/` — reproducible source dataset and forecasting pipeline
- `docs/` — project and responsible AI documentation
- Root `.pptx` files — hackathon submission material

## Run locally

### Web app

```bash
cd web
npm ci
npm run dev
```

Open http://localhost:3000. Production build: `npm run build`; start with `npm run start`.

### FastAPI service

```bash
cd backend
python -m venv .venv
# Activate the environment, then:
pip install -r requirements.txt
uvicorn main:app --reload --port 8000
```

API docs are at http://localhost:8000/docs and health is at `/health`.

### Offline dashboard and data pipeline

Open `dashboard/index.html` in a browser. To regenerate the prototype data:

```bash
python data/generate_dataset.py
python model/ai_pipeline.py
```

## Deploy on Railway

Deploy the web app and API as two services from this GitHub repository:

1. Create a Railway project and add a service from this GitHub repository.
2. For the web service, set **Root Directory** to `/web`. Railway uses `web/railway.json`; its health check is `/api/health`.
3. Add a second service from the same repository and set **Root Directory** to `/backend`. Railway uses `backend/railway.json`; its health check is `/health`.
4. Generate a public domain for each service in Railway Networking settings.

Both services bind to Railway's injected `$PORT`. No database or environment variables are required for the prototype. To deploy only the web app, configure just the `/web` service. Railway configuration files are also provided next to each service for deployments configured via their respective root directories.

## Demo account

The prototype login uses demo credentials as described in the application. Do not use demo credentials or illustrative data for real health decisions.
