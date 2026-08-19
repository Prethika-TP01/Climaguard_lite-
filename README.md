# ClimaGuard Lite

## AI-Assisted Urban Flood Risk & Response Platform

### Target City
Coimbatore, Tamil Nadu

ClimaGuard Lite is a college project designed to provide an early, zone-level understanding of urban flood risk.

The system combines:

- Rainfall data
- Flood-risk prediction
- Rainfall anomaly detection
- Citizen reports
- NLP-based report triage
- Multi-signal priority calculation
- Explainable flood priority
- Interactive Coimbatore map

## Main Questions

The system aims to answer:

1. WHERE is the risk?
2. WHY is the area risky?
3. WHICH area needs attention FIRST?

## Project Pipeline

Predict → Detect → Understand → Prioritize → Inform

## Three Main Modules

### Module 1 — Rainfall & Flood Risk Engine

Responsible for:

- Rainfall data
- Data processing
- Feature engineering
- Flood-risk prediction
- Risk scoring
- Rainfall anomaly detection

### Module 2 — Citizen Intelligence & Priority Engine

Responsible for:

- Citizen reports
- NLP classification
- Category detection
- Severity
- Urgency
- Citizen score
- Priority calculation
- Explainability

### Module 3 — Map & Decision Dashboard

Responsible for:

- Coimbatore map
- Risk zones
- Rainfall anomaly visualization
- Citizen report markers
- Priority visualization
- Dashboard statistics
- Zone details
- Risk explanation

## Technologies

- HTML
- CSS
- JavaScript
- Leaflet.js
- Python
- Flask
- Pandas
- Scikit-learn
- Hugging Face Transformers
- Open-Meteo API

## Project Structure

```text
Climaguard_lite-
│
├── frontend/
├── backend/
│   ├── api/
│   ├── models/
│   └── services/
│       ├── risk/
│       ├── reports/
│       └── priority/
├── ml/
├── nlp/
├── data/
├── tests/
├── docs/
│
├── README.md
├── SPEC.md
├── CONTRIBUTING.md
├── requirements.txt
├── .gitignore
└── .env.example