# Google Search Engine CTR & Engagement Opportunity Scoring

[![Deploy Paper to GitHub Pages](https://github.com/aadesh07-source/Google-search-engine-for-CTR-Engagement-Opportunity/actions/workflows/deploy.yml/badge.svg)](https://github.com/aadesh07-source/Google-search-engine-for-CTR-Engagement-Opportunity/actions/workflows/deploy.yml)
[![CI](https://github.com/aadesh07-source/Google-search-engine-for-CTR-Engagement-Opportunity/actions/workflows/ci.yml/badge.svg)](https://github.com/aadesh07-source/Google-search-engine-for-CTR-Engagement-Opportunity/actions/workflows/ci.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Python: 3.11+](https://img.shields.io/badge/Python-3.11%2B-blue)](backend/pyproject.toml)
[![React: 18](https://img.shields.io/badge/Frontend-React%2018%20%7C%20Vite-61dafb)](frontend/package.json)

> **Research Paper & Decision-Support System**: An end-to-end Machine Learning scoring engine and interactive web publication for identifying high-opportunity content in Google search results based on click-through rate (CTR), engagement dynamics, and rank efficiency.

---

## 🌐 Live Research Paper & Web Application

The interactive research paper and decision-support tool are deployed on GitHub Pages:
👉 **[View Live Web Research Paper](https://aadesh07-source.github.io/Google-search-engine-for-CTR-Engagement-Opportunity/)**

---

## 🎯 Research Framing & Problem Statement

Organic search performance workflows frequently suffer from three fundamental failures:
1. **Rank as Proxy**: Assuming high SERP ranking guarantees high traffic, neglecting snippet attractiveness and SERP feature occlusion.
2. **CTR in a Vacuum**: Treating CTR in isolation from impressions and downstream engagement (e.g., bounce rates, time on page, scroll depth).
3. **Uncalibrated Heuristics**: Relying on arbitrary threshold rules rather than calibrated probabilistic opportunity models.

This project implements a **leakage-safe, decision-theoretic ML framework** that:
- Employs empirical Bayesian smoothing on sparse impression CTRs.
- Formulates pre-intervention and post-intervention temporal windows to guarantee zero look-ahead bias.
- Compares a transparent baseline scoring rule against gradient-boosted decision trees (LightGBM).
- Delivers an actionable review queue with calibrated probability scores, confidence bands, interpretable reason codes, and prescriptive interventions.

---

## 🔬 Key Empirical Results

| Metric | Rule Baseline | LightGBM Model | Relative Gain |
|---|---|---|---|
| **PR-AUC** | 0.612 | **0.741** | **+21.1%** |
| **Precision @ 20** | 0.700 | **0.850** | **+21.4%** |
| **Precision @ 50** | 0.680 | **0.820** | **+20.6%** |
| **Brier Score** (Calibration) | 0.184 | **0.112** | **-39.1%** |
| **Expected Calibration Error (ECE)** | 0.089 | **0.038** | **-57.3%** |

---

## 🏗️ Repository Architecture

This project is structured as an integrated full-stack machine learning solution:

```text
├── submission/
│   ├── paper_url.txt                 # Canonical deployed research paper URL
│   └── README.md
├── frontend/                         # React 18 + Vite interactive research paper & UI
│   ├── src/
│   │   ├── sections/                 # Modular paper sections (Abstract, Intro, Methodology,
│   │   │                             # Results, Recommendations, Limitations, Reproducibility)
│   │   ├── components/               # Interactive charts, Recharts cards, TanStack table
│   │   ├── api/                      # Data client (static JSON fallback or FastAPI backend)
│   │   └── index.css                 # Responsive design system
│   ├── public/data/                  # Static precomputed model artifacts & metrics
│   └── vite.config.js                # Vite build config with GitHub Pages routing
├── backend/                          # FastAPI REST API & ML Pipeline
│   ├── app/
│   │   ├── api/                      # REST endpoints (/meta, /eda, /results, /recommendations)
│   │   ├── schemas/                  # Pydantic response models
│   │   └── services/                 # Artifact loading & validation layer
│   ├── pipeline/                     # Modular ML pipeline
│   │   ├── load.py                   # Secure dataset ingest
│   │   ├── clean.py                  # Deduplication & anomaly handling
│   │   ├── windows.py                # Pre/post observation window framing
│   │   ├── features.py               # Feature derivation & Bayesian smoothing
│   │   ├── labels.py                 # Multi-condition opportunity labeling
│   │   ├── split.py                  # Client-grouped temporal cross-validation split
│   │   ├── baseline.py               # Rule-based reference engine
│   │   ├── model.py                  # LightGBM classifier with isotonic calibration
│   │   ├── evaluate.py               # PR curves, calibration, and rank metrics
│   │   └── score.py                  # Scoring engine & reason code generator
│   ├── scripts/                      # Static artifact exporters & public privacy scanner
│   └── tests/                        # Data leakage prevention & unit test suite
├── artifacts/public/                 # Exported JSON artifacts for client applications
├── config/                           # schema.yaml & params.yaml configuration
├── scripts/                          # Python CLI runners (01_prepare to 04_evaluate)
└── .github/workflows/
    ├── deploy.yml                    # Automated GitHub Pages build & deploy
    └── ci.yml                        # Full-stack automated unit & integration testing
```

---

## 🔒 Public Safety & Privacy by Design

- **Zero Client Identifiers**: All content and client identifiers are pseudonymized with salted SHA-256 hashes (`content_id`, `client_id`).
- **No Raw Data Commits**: No raw proprietary datasets, URLs, domains, page titles, or raw queries are committed to this repository.
- **Privacy Scanner**: An automated scan (`backend/scripts/scan_public.py`) validates that all exported artifacts contain only aggregate and pseudonymized data.

---

## 💻 Quick Start & Local Development

### 1. Backend (FastAPI & ML Pipeline)

```bash
# Clone the repository
git clone https://github.com/aadesh07-source/Google-search-engine-for-CTR-Engagement-Opportunity.git
cd Google-search-engine-for-CTR-Engagement-Opportunity

# Install Python dependencies
pip install -r requirements.txt
pip install -e backend

# Run the test suite
pytest backend/tests

# Launch the FastAPI service (runs on http://127.0.0.1:8000)
uvicorn backend.app.main:app --reload
```

Interactive Swagger documentation is available at `http://127.0.0.1:8000/docs`.

### 2. Frontend (React 18 + Vite)

```bash
# Navigate to the frontend directory
cd frontend

# Install Node dependencies
npm install

# Start the development server (runs on http://localhost:5173)
npm run dev

# Run frontend tests
npm test

# Build the production bundle
npm run build
```

---

## 📜 Acknowledgments & Data Credit

- Research foundation and search intelligence dataset provided by [FlyRank](https://flyrank.ai).
- Machine Learning methodology adheres to reproducible, leakage-free decision-support standards.
