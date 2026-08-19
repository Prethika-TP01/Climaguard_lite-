# ClimaGuard Lite
## AI-Assisted Urban Flood Risk & Response Platform

### Target City
Coimbatore, Tamil Nadu

### Project Type
AI/ML + NLP + Web Dashboard

---

# 1. Problem Statement

Urban areas such as Coimbatore can experience waterlogging and flooding during periods of heavy or abnormal rainfall. Existing information is often fragmented between weather data, flood-risk information and citizen observations.

ClimaGuard Lite aims to provide an early, zone-level view of urban flood risk by combining rainfall-based prediction, rainfall anomaly detection and citizen-reported ground information.

The system will help answer:

> Which area needs attention first, why is it at risk, and what is happening there?

---

# 2. Core Concept

ClimaGuard Lite follows this pipeline:

Predict → Detect → Understand → Prioritize → Inform

The system combines:

Rainfall Data
+
Flood Risk Prediction
+
Rainfall Anomaly Detection
+
Citizen Reports
+
NLP Triage
=
Explainable Flood Priority

---

# 3. Main Differentiator

ClimaGuard Lite should not only predict whether an area may experience flood risk.

It should combine predicted risk with real-world citizen reports.

Core concept:

Predicted Risk + Rainfall Anomaly + Citizen Ground Truth
→ Explainable Priority

Example:

High predicted risk
+
Abnormal rainfall
+
Multiple citizen reports
+
Urgent reports

↓

CRITICAL PRIORITY

The system should explain WHY an area has been classified as high or critical.

---

# 4. System Architecture

The project is divided into 3 independent modules.

## Module 1 — Rainfall & Flood Risk Engine

Question answered:

> Will this area be risky?

Responsibilities:

- Collect rainfall data
- Process historical rainfall
- Process recent/current rainfall
- Prepare Coimbatore zone data
- Feature engineering
- Flood-risk prediction
- Risk scoring
- Risk classification
- Rainfall anomaly detection
- Provide risk data through API

---

## Module 2 — Citizen Intelligence & Priority Engine

Question answered:

> What is actually happening there, and how urgent is it?

Responsibilities:

- Citizen report submission
- Free-text report processing
- NLP classification
- Category detection
- Severity detection
- Urgency detection
- Citizen report aggregation
- Ground-truth score
- Final priority calculation
- Explainable priority reasons

---

## Module 3 — Map & Decision Dashboard

Question answered:

> Where is the problem, and how do we visualize and prioritize it?

Responsibilities:

- Interactive Coimbatore map
- Flood-risk visualization
- Rainfall anomaly visualization
- Citizen report markers
- Priority visualization
- Dashboard statistics
- Zone details
- Explanation of risk
- Situation timeline

---

# 5. Module 1 — Risk Engine

## Inputs

The module may use:

- Historical rainfall
- Recent rainfall
- Historical rainfall statistics
- Zone information
- Low-lying indicator
- Historical flood indicator

For the prototype, heuristic/rule-assisted labels may be used where verified flood labels are unavailable.

These must be clearly identified as prototype labels and not presented as verified real-world observations.

---

## Risk Score

The model should generate:

0–100 risk score.

Initial classification:

0–39   = LOW

40–69  = MEDIUM

70–84  = HIGH

85–100 = CRITICAL

---

## Rainfall Anomaly

Initial formula:

Anomaly Ratio =
Current Rainfall / Historical Expected Rainfall

Initial classification:

< 1.2       = NORMAL

1.2–1.5     = ELEVATED

1.5–2.0     = HIGH

> 2.0       = SEVERE

These thresholds are prototype defaults and may be adjusted after testing.

---

## Module 1 Output

The API should return data in this structure:

{
  "zone_id": "CBE_001",
  "zone_name": "Gandhipuram",
  "risk_score": 82,
  "risk_level": "HIGH",
  "rainfall": 82,
  "expected_rainfall": 45,
  "anomaly_ratio": 1.82,
  "anomaly_level": "HIGH"
}

---

# 6. Module 2 — Citizen Intelligence

## Citizen Report

A citizen can submit:

- Description
- Location
- Timestamp
- Category
- Optional image

Initial categories:

- Waterlogging
- Road Flooding
- House Flooding
- Drainage Overflow
- Heavy Rainfall
- Other

---

## NLP Triage

The NLP system should identify:

- Category
- Severity
- Urgency
- Short summary

Example:

Input:

"Water has entered several houses and vehicles cannot pass."

Output:

Category: House Flooding
Severity: HIGH
Urgency: CRITICAL

---

# 7. Citizen Ground-Truth Score

The system should calculate a citizen signal using:

- Number of reports
- Number of urgent reports
- Report severity
- Report concentration within a zone

Example:

Total reports: 7

Urgent reports: 3

Citizen Score: 85/100

---

# 8. Priority Engine

The priority engine combines multiple signals.

Initial weights:

Flood Risk        = 40%

Rainfall Anomaly  = 20%

Citizen Reports   = 20%

Urgent Reports    = 15%

Vulnerability     = 5%

All values should be normalized to 0–100.

---

## Priority Classification

0–39     = LOW

40–59    = MODERATE

60–79    = HIGH

80–100   = CRITICAL

---

## Priority Output

Example:

{
  "zone_id": "CBE_001",
  "citizen_reports": 7,
  "urgent_reports": 3,
  "citizen_score": 85,
  "priority_score": 88,
  "priority_level": "CRITICAL",
  "reasons": [
    "High predicted flood risk",
    "High rainfall anomaly",
    "Multiple citizen reports",
    "Multiple urgent reports"
  ]
}

---

# 9. Module 3 — Dashboard

The dashboard should contain:

- Coimbatore map
- Risk zones
- Rainfall anomaly layer
- Citizen report markers
- Priority layer
- Dashboard statistics
- Zone details
- Risk explanation
- Situation timeline

---

## Dashboard Statistics

Display:

Current Rainfall

Rainfall Anomaly

Low-Risk Zones

Medium-Risk Zones

High-Risk Zones

Critical Zones

Citizen Reports

Urgent Reports

---

# 10. Zone Details

When a user selects a zone:

Example:

Zone: Gandhipuram

Risk Score: 82/100

Risk Level: HIGH

Rainfall: 82 mm

Expected Rainfall: 45 mm

Anomaly: 1.82×

Citizen Reports: 7

Urgent Reports: 3

Final Priority: CRITICAL

---

# 11. Explainability

For every High/Critical zone, show why it received that classification.

Example:

WHY CRITICAL?

- Rainfall is significantly above normal
- Predicted flood risk is high
- Multiple citizen reports received
- Multiple reports are urgent
- Zone has higher vulnerability

The exact reasons should be generated from the actual signals used by the system.

---

# 12. API CONTRACT

The three modules must communicate through clearly defined APIs.

## Module 1 APIs

GET /api/zones

GET /api/risk

GET /api/anomalies

---

## Module 2 APIs

POST /api/reports

GET /api/reports

POST /api/reports/analyze

GET /api/priorities

GET /api/zone/{zone_id}/priority

---

## Module 3

The dashboard consumes the APIs from Modules 1 and 2.

---

# 13. Required Data Contract

Risk data must follow:

{
  "zone_id": "CBE_001",
  "zone_name": "Gandhipuram",
  "risk_score": 82,
  "risk_level": "HIGH",
  "rainfall": 82,
  "expected_rainfall": 45,
  "anomaly_ratio": 1.82,
  "anomaly_level": "HIGH"
}

Priority data must follow:

{
  "zone_id": "CBE_001",
  "citizen_reports": 7,
  "urgent_reports": 3,
  "citizen_score": 85,
  "priority_score": 88,
  "priority_level": "CRITICAL"
}

Field names should not be changed without agreement from all team members.

---

# 14. Repository Structure

ClimaGuard-Lite/

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

├── README.md

├── SPEC.md

├── CONTRIBUTING.md

├── .gitignore

└── .env.example

---

# 15. Team Ownership

## Team Member 1 — Risk Engine

Owns:

ml/

backend/services/risk/

Responsible for:

- Rainfall data
- Data processing
- Feature engineering
- ML model
- Risk prediction
- Risk score
- Rainfall anomaly

Branch:

feature/risk-engine

---

## Team Member 2 — Citizen Intelligence

Owns:

nlp/

backend/services/reports/

backend/services/priority/

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

feature/citizen-ai

---

## Team Member 3 — Dashboard

Owns:

frontend/

Responsible for:

- React UI
- Leaflet map
- Risk visualization
- Anomaly visualization
- Citizen markers
- Dashboard
- Zone details
- Timeline

Branch:

feature/dashboard

---

# 16. Git Collaboration Rules

The main branches are:

main
develop

Feature branches:

feature/risk-engine

feature/citizen-ai

feature/dashboard

No team member should directly develop on main.

Work should follow:

Feature Branch
→ Pull Request
→ develop
→ Integration Testing
→ main

---

# 17. File Ownership Rule

Team members should avoid modifying another member's module.

Person 1:

ml/

backend/services/risk/

Person 2:

nlp/

backend/services/reports/

backend/services/priority/

Person 3:

frontend/

Shared files such as API contracts, requirements and configuration should be changed carefully and communicated to the team.

---

# 18. Development Rules

1. Follow SPEC.md.
2. Do not randomly change API field names.
3. Do not commit API keys.
4. Use .env for secrets.
5. Test each module independently.
6. Pull the latest develop branch before starting work.
7. Create Pull Requests instead of directly pushing to main.
8. Run tests before creating a Pull Request.
9. Keep commits small and descriptive.
10. Do not overwrite another team member's work.

---

# 19. Testing Requirements

Each module must have independent tests.

Required tests include:

- Risk score range validation
- Risk classification
- Rainfall anomaly calculation
- NLP classification
- Severity/urgency output
- Priority score calculation
- API response validation
- Frontend API integration

---

# 20. Integration Test

The complete system must support:

Rainfall Data

↓

Risk Engine

↓

Risk + Anomaly API

↓

Citizen Reports + NLP

↓

Priority Engine

↓

Priority API

↓

Dashboard

↓

Coimbatore Flood Risk Map

---

# 21. Example Complete Flow

Rainfall:

82 mm

↓

Expected rainfall:

45 mm

↓

Anomaly:

1.82×

↓

Risk Score:

82 HIGH

↓

Citizen Reports:

7

↓

Urgent Reports:

3

↓

Priority Score:

88

↓

Final Priority:

CRITICAL

↓

Dashboard:

Gandhipuram displayed as CRITICAL

↓

Dashboard explains:

- High predicted risk
- High rainfall anomaly
- Multiple citizen reports
- Multiple urgent reports

---

# 22. MVP

The first working version must contain:

- Coimbatore map
- Zone-level risk
- Rainfall data
- Rainfall anomaly
- Citizen report submission
- NLP report classification
- Severity/urgency
- Multi-signal priority
- Explainable risk
- Dashboard

Future features should only be added after the MVP works reliably.

---

# 23. Future Enhancements

Possible future features:

- More cities
- Real-time sensors
- Image-based flood verification
- SMS/notification system
- Evacuation route suggestions
- Authority dashboard
- Historical flood analytics
- Mobile application
- More advanced flood modelling

---

# 24. Final Product Vision

ClimaGuard Lite should answer three questions:

1. WHERE is the risk?
2. WHY is the area risky?
3. WHICH area needs attention FIRST?

Final pipeline:

Predict
→ Detect
→ Understand
→ Prioritize
→ Inform