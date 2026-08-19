# Contributing to ClimaGuard Lite

## Branches

The project uses:

- `main` — stable version
- `develop` — integration branch

Feature branches:

- `feature/risk-engine`
- `feature/citizen-ai`
- `feature/dashboard`

## Development Flow

Feature Branch
→ Pull Request
→ develop
→ Integration Testing
→ main

## Rules

1. Do not work directly on `main`.
2. Work on your assigned feature branch.
3. Follow `SPEC.md`.
4. Do not randomly change API field names.
5. Do not commit API keys or passwords.
6. Use `.env` for secrets.
7. Test your changes before creating a Pull Request.
8. Pull the latest `develop` before starting new work.
9. Keep commits small and descriptive.
10. Do not overwrite another team member's module.

## Team Ownership

### Person 1 — Risk Engine

Owns:

- `ml/`
- `backend/services/risk/`

Responsible for:

- Rainfall data
- Data processing
- Feature engineering
- ML model
- Risk prediction
- Risk score
- Rainfall anomaly

Branch:

`feature/risk-engine`

### Person 2 — Citizen Intelligence

Owns:

- `nlp/`
- `backend/services/reports/`
- `backend/services/priority/`

Responsible for:

- Citizen reports
- NLP
- Category
- Severity
- Urgency
- Citizen score
- Priority engine
- Explainability

Branch:

`feature/citizen-ai`

### Person 3 — Dashboard

Owns:

- `frontend/`

Responsible for:

- Dashboard UI
- Leaflet map
- Risk visualization
- Anomaly visualization
- Citizen markers
- Zone details
- Timeline

Branch:

`feature/dashboard`

## File Ownership

Team members should avoid modifying another member's module.

Shared files such as API contracts, requirements and configuration should be changed carefully and communicated to the team.

## Testing

Each module must be tested independently before creating a Pull Request.

Required tests include:

- Risk score validation
- Risk classification
- Rainfall anomaly calculation
- NLP classification
- Severity and urgency
- Priority score calculation
- API response validation
- Frontend API integration