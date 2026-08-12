# ⚡ PulseForge — AI-Powered Hackathon Management Platform

[![FastAPI](https://img.shields.io/badge/FastAPI-005571?style=for-the-badge&logo=fastapi)](https://fastapi.tiangolo.com)
[![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)](https://react.dev)
[![Gemini](https://img.shields.io/badge/Google%20Gemini-8E75C2?style=for-the-badge&logo=googlegemini&logoColor=white)](https://ai.google.dev)
[![SQLite](https://img.shields.io/badge/SQLite-07405E?style=for-the-badge&logo=sqlite&logoColor=white)](https://sqlite.org)

PulseForge is an AI-powered end-to-end hackathon lifecycle management dashboard. It automates registration, team formation, project submission, reviewer assignments, and bias-aware evaluation with fully transparent, auditable statistical methods and Gemini-driven intelligence.

Designed to solve the fragmented workflow of hackathon organization (which typically requires 5-7 disconnected tools), PulseForge integrates everything into a single, cohesive dashboard with clear analytics and audit logs.

---

## 🚀 Key Features

### 1. Multi-Objective Reviewer Assignment
* **Greedy Optimization Engine (`/api/reviewers/assign`):** Automatically distributes projects to reviewers by balancing:
  * **Expertise Alignment (40%):** Matches reviewer's tags with project technologies.
  * **Workload Distribution (30%):** Ensures no reviewer gets overloaded.
  * **Conflict-of-Interest Avoidance (20%):** Hard exclusion of reviewers from matching teams/organizations.
  * **Diversity (10%):** Maximizes diverse domain exposure.
* **Explainability:** Every assignment is stored alongside its precise scoring breakdown.

### 2. Statistical Bias Detection & Score Normalization
* **Z-Score Normalization (`/api/evaluations/normalize`):** Automatically adjusts raw scores to counter reviewer harshness or leniency.
* **Bias Scan (`/api/evaluations/bias-scan`):** Flags statistically significant scoring gaps across:
  * **Gender** & **Geography**
  * **Institution** & **Tech Stack**
* **Auditability:** Every flag is backed by real z-statistics and confidence calculations, ensuring 100% mathematical auditability with zero opaque ML models.

### 3. Smart Duplicate & Skill Extraction
* **Fuzzy Match Engine (`/api/duplicates/check/*`):** Performs exact-email, fuzzy-name (Token Sort Ratio), and organization-based duplicate checks.
* **AI-Assisted Skill Extraction (`/api/skills/extract`):** Parses free-text bios/skills into a standardized taxonomy using Google Gemini.
* **Deterministic Fallback:** A robust, regex-based offline keyword parser takes over if the Gemini API key is missing or rate-limited.

---

## 📂 System Architecture

```
hackbridgecode/
├── app/                  # Backend Application (FastAPI)
│   ├── core/             # Configuration & DB Engine
│   ├── models/           # SQLAlchemy ORM Models
│   ├── schemas/          # Pydantic Schemas (Request/Response validation)
│   ├── repositories/     # Data Access Layer (clean DB operations)
│   ├── services/         # Business Logic, Optimization & Normalization Algorithms
│   ├── routers/v1/       # REST API Endpoints
│   └── utils/            # Gemini client, Security, Roles, and Fuzzy Logic
├── frontend/1/           # Frontend Application (React + Vite + TypeScript)
│   ├── src/
│   │   ├── components/   # Modern, highly visual dashboard components
│   │   ├── utils/        # API callers & local storage auth handlers
│   │   └── types.ts      # TypeScript interfaces
├── scripts/              # Migration, DB patching, and Seed scripts
└── tests/                # Comprehensive Test Suite (pytest)
```

**Architectural Principle:** Strict layer boundary segregation (`Router → Service → Repository → Model`). Routers never interact with the database directly, ensuring codebase maintainability.

---

## 🛠️ Installation & Setup

### Backend Setup (FastAPI)

1. **Clone & Navigate:**
   ```bash
   cd hackbridgecode
   ```

2. **Initialize Virtual Environment:**
   ```bash
   python3 -m venv venv
   source venv/bin/activate  # On Windows use: venv\Scripts\activate
   ```

3. **Install Dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Environment Variables:**
   Create a `.env` file in the root directory:
   ```env
   GEMINI_API_KEY=your_gemini_api_key_here
   DATABASE_URL=sqlite:///./pulseforge.db
   ```
   *Note: If no Gemini API key is provided, the application will automatically fall back to the offline keyword skill extractor.*

5. **Seed the Database:**
   Populate the database with a realistic mock dataset containing intentionally baked-in bias anomalies for demoing purposes:
   ```bash
   python -m scripts.seed_data
   ```

6. **Run Server:**
   ```bash
   uvicorn app.main:app --reload
   ```
   Interactive Swagger docs will be available at `http://localhost:8000/docs`.

---

### Frontend Setup (React + Vite)

1. **Navigate to Frontend:**
   ```bash
   cd frontend/1
   ```

2. **Install Packages:**
   ```bash
   npm install
   ```

3. **Configure Environment:**
   Create a `.env.local` file:
   ```env
   VITE_API_URL=http://localhost:8000
   ```

4. **Run Live Server:**
   ```bash
   npm run dev
   ```
   Open `http://localhost:5173` to explore the dashboard.

---

## 🧪 Testing

PulseForge features an extensive test suite verifying mathematical correctness, security boundaries, and optimizer outputs.

To run tests in an isolated, in-memory SQLite database environment:
```bash
pytest tests/ -v
```

---

## 📐 Design Decisions & Trade-offs

* **Greedy Optimizer vs. Integer Linear Programming (ILP):** Instead of utilizing heavy constraint programming (like `scipy.optimize`), a greedy multi-objective algorithm was chosen. It scales at $O(\text{projects} \times \text{reviewers})$, completes in milliseconds for $1000+$ items, and allows storing exact score justification metrics.
* **Statistical Normalization vs. Machine Learning:** Z-score normalization and standard deviation comparisons require zero pre-training or massive labeled datasets, making them perfect for newly launched hackathons.
* **SQLite Out-Of-The-Box:** SQLite enables instant local execution. Because database queries are isolated inside the `repositories` layer, changing to a production PostgreSQL database simply requires modifying the `DATABASE_URL` environment variable.
