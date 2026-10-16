# 🎓 University Timetable Optimizer (UniOptima)
> **SC05 M1 Capstone Project** &bull; Automated Combinatorial Optimization for Academic Scheduling

UniOptima is an automated University Timetable Optimization system designed to solve high-dimensional academic scheduling problems. It provides a comparative benchmark between a deterministic **Greedy Baseline Heuristic** (Most Constrained Variable First) and a metaheuristic **Genetic Algorithm Optimizer** under strict hard physical constraints and multi-objective soft quality preferences.

---

## 🌟 Key Features
- **Hard Constraint Enforcement:** Guarantees zero room double-booking, zero faculty time overlaps, zero student cohort concurrent classes, room capacity compliance, lab room equipment verification, and faculty workday availability.
- **Multi-Objective Soft Optimization:** Minimizes student idle gap hours, distributes multi-credit courses evenly across weekdays, balances faculty daily teaching hours, and maximizes room seating utilization.
- **Comparative Algorithm Benchmarking:** Side-by-side performance evaluation measuring fitness scores, constraint violation counts, compute execution time (ms), and generational convergence curves.
- **FastAPI Python Backend:** Clean, modular REST API with Pydantic v2 validation, CORS support, static asset serving, and automatic OpenAPI documentation.
- **Vanilla Modern Frontend:** Responsive glassmorphic single-page web app built purely with HTML5, CSS3 design tokens, and Vanilla JavaScript—no external frontend framework build steps required.
- **Standardized CSV Ingestion:** Ingests courses, rooms, faculty, cohorts, and timeslots with dynamic validation and CSV schedule export.

---

## 📂 Project Folder Structure

```text
university-timetable-optimizer/
├── README.md                      # Comprehensive capstone project documentation
├── requirements.txt               # Backend dependencies (FastAPI, uvicorn, pytest, etc.)
├── .gitignore                     # Git ignore rules for Python, IDE, and test artifacts
├── backend/                       # Python FastAPI Backend
│   ├── app/
│   │   ├── main.py                # FastAPI entry point, CORS, routes & static mounting
│   │   ├── models/
│   │   │   ├── __init__.py
│   │   │   └── timetable_models.py# Domain dataclasses (Course, Room, Faculty, Assignment)
│   │   ├── schemas/
│   │   │   ├── __init__.py
│   │   │   └── timetable_schemas.py# Pydantic v2 request/response schemas
│   │   ├── routes/
│   │   │   ├── __init__.py
│   │   │   └── timetable_routes.py# Endpoints: /data, /schedule/baseline, /schedule/genetic, /compare, /export
│   │   ├── services/
│   │   │   ├── __init__.py
│   │   │   ├── baseline_scheduler.py # Deterministic Greedy Degree Heuristic
│   │   │   ├── genetic_algorithm.py  # Metaheuristic GA with Tournament Selection & Elitism
│   │   │   └── fitness.py            # Objective penalty & fitness evaluation engine
│   │   ├── database/
│   │   │   ├── __init__.py
│   │   │   └── data_loader.py        # CSV dataset loader with fallbacks
│   │   └── validators/
│   │       ├── __init__.py
│   │       └── constraint_validator.py# Hard and soft constraint rules engine
│   └── tests/                     # Automated Pytest Suite
│       ├── __init__.py
│       ├── test_baseline.py       # Baseline heuristic unit tests
│       ├── test_genetic.py        # Genetic algorithm execution tests
│       ├── test_constraints.py    # Hard/soft constraint rule validation tests
│       └── test_api.py            # FastAPI TestClient endpoint integration tests
├── frontend/                      # Client UI (HTML5, Vanilla CSS, Vanilla JavaScript)
│   ├── index.html                 # Main dashboard with stats, grid, and benchmark views
│   ├── pages/
│   │   ├── timetable-view.html    # Modular timetable grid view template
│   │   ├── comparison-view.html   # Modular benchmark & convergence view template
│   │   └── dataset-view.html      # Modular dataset explorer view template
│   ├── css/
│   │   └── style.css              # Custom HSL dark theme, glassmorphism, responsive grid
│   ├── js/
│   │   └── app.js                 # Frontend state management, API client & canvas charts
│   └── assets/
│       └── logo.svg               # Scalable SVG application logo
├── data/                          # Benchmark Datasets in CSV format
│   ├── README.md                  # Dataset dictionary and schema documentation
│   ├── courses.csv                # Courses, credit requirements, lab requirements
│   ├── rooms.csv                  # Classrooms, labs, seating capacities
│   ├── faculty.csv                # Faculty names, max load, available workdays
│   ├── cohorts.csv                # Student batches/sections and student headcount
│   └── timeslots.csv              # Monday to Friday time periods (09:00 - 15:30)
├── docs/                          # Architectural & Design Documentation
│   ├── STEP-1.md                  # Milestone 1 problem formulation & mathematical model
│   ├── baseline-pseudocode.md     # Greedy baseline pseudocode and complexity analysis
│   ├── genetic-algorithm.md       # GA chromosome encoding and operator design
│   └── product-v1-sketch.png      # System architecture and UI flow diagram
└── results/                       # Experimental Artifacts & Outputs
    ├── charts/
    │   └── convergence_comparison.png # Generational convergence plot
    └── reports/
        ├── README.md
        └── benchmark_report_sample.json # Sample execution metrics and benchmark JSON
```

---

## 🚀 How to Run the Project

### 1. Prerequisites
- Python 3.10+ (Tested on Python 3.13)
- Modern web browser (Chrome, Edge, Firefox, Safari)

### 2. Install Dependencies
Open a terminal in the `university-timetable-optimizer` directory:
```bash
pip install -r requirements.txt
```

### 3. Run the Backend API Server
Start the FastAPI server with Uvicorn:
```bash
uvicorn backend.app.main:app --reload --host 127.0.0.1 --port 8000
```
- API Base URL: `http://127.0.0.1:8000`
- Interactive OpenAPI Docs: `http://127.0.0.1:8000/docs`
- Health Check: `http://127.0.0.1:8000/api/health`

### 4. Launch the Frontend
You have two options:
1. **Direct Browser Access:** Open `frontend/index.html` directly in your browser. (The JavaScript auto-detects `http://127.0.0.1:8000` for API calls).
2. **Via FastAPI Server:** Navigate to `http://127.0.0.1:8000/static/index.html` while the backend is running.

### 5. Run Automated Tests
Execute the full Pytest suite:
```bash
python -m pytest backend/tests -v
```

---

## ⚡ API Endpoint Reference

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/health` | Service health status check |
| `GET` | `/api/data` | Retrieves parsed courses, rooms, faculty, cohorts, and timeslots |
| `POST` | `/api/schedule/baseline` | Executes deterministic Greedy Baseline scheduler |
| `POST` | `/api/schedule/genetic` | Executes Genetic Algorithm with configurable hyperparameters |
| `POST` | `/api/schedule/compare` | Runs live comparative benchmark between Baseline and GA |
| `POST` | `/api/validate` | Validates custom assignment lists against all constraints |
| `GET` | `/api/export/csv` | Exports the latest generated timetable schedule to CSV |

---

## 🧪 Optimization Algorithms

### 1. Greedy Baseline (Deterministic Heuristic)
- Expands course credits into atomic 1-hour sessions.
- Sorts sessions using **Most Constrained Variable First (MCVF)**:
  1. Lab courses prioritized over general classrooms.
  2. Large cohorts prioritized over smaller sections.
  3. Faculty with fewer available workdays prioritized.
- Greedily locks the best feasible, clash-free timeslot and room.
- Complexity: $O(N \log N + N \times K \times M)$ with sub-5ms runtime.

### 2. Genetic Algorithm (Metaheuristic Optimizer)
- **Chromosome Representation:** Vector of genes $\langle \text{Course}, \text{Room}, \text{Timeslot} \rangle$.
- **Selection:** Tournament selection ($k = 4$) maintains exploration diversity.
- **Crossover:** Uniform crossover ($P_c = 0.85$) recombines parent sub-schedules.
- **Mutation:** Random gene perturbation ($P_m = 0.15$) alters room or timeslot.
- **Elitism:** Top 2 individuals preserved directly each generation to ensure non-decreasing fitness.
- Tracks generational best fitness and population average for convergence analysis.

---

## 📄 License
Academic Capstone Project &bull; SC05 Milestone 1
