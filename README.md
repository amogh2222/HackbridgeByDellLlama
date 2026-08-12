# HackBridge

[FastAPI](https://img.shields.io/badge/FastAPI-005571?style=flat-square)
[React](https://img.shields.io/badge/React-20232A?style=flat-square)
[Google Gemini](https://img.shields.io/badge/Google_Gemini-8E75C2?style=flat-square)
[SQLite](https://img.shields.io/badge/SQLite-07405E?style=flat-square)

A unified hackathon administration platform replacing fragmented coordination tools with a mathematically transparent API surface.

---

## Unique Selling Proposition (USP) & Differentiation

> **100% Explainable Audit Trails**  
> PulseForge entirely avoids "black-box" machine learning. Scoring, reviewer assignments, and group bias normalizations are calculated using transparent Z-scores and greedy multi-objective optimization, allowing organizers to trace, justify, and verify every single decision.

> **Resilient Local Fallback**  
> Combines Google Gemini API skill extraction with a local regex-based fallback keyword parser. If external networks or API limits drop during judging, the application automatically switches to local parsing and continues running without interruption.

---

## Technical Stack

| Layer | Technology | Purpose |
| :--- | :--- | :--- |
| **Backend** | FastAPI | High-performance asynchronous REST API routing |
| **Frontend** | React + Vite + TypeScript | Responsive admin dashboard with Tailwind CSS styling |
| **Database** | SQLite + SQLAlchemy | Embedded relational storage with strict Repository isolation |
| **Fuzzy Matching** | RapidFuzz | Exact-email and fuzzy-name matching algorithms |
| **AI Integration** | Google Gemini API | Adaptive participant skill extraction and taxonomy tagging |

---

## Pipeline Flow

```
[Registration] ──> [Fuzzy Duplicate Check] ──> [Skill Extraction] ──> [Reviewer Assignment] ──> [Bias Normalization]
```

* **Fuzzy Duplicate Check:** Cross-references exact emails, fuzzy names (token sort ratio), and organization matches.
* **Skill Extraction:** Standardizes participant bios into a clean technology taxonomy.
* **Reviewer Assignment:** Greedy optimizer balancing expertise (40%), workload (30%), COI exclusion (20%), and diversity (10%).
* **Bias Normalization:** Calculates reviewer-level Z-scores to normalize harsh/lenient evaluations across cohorts.
