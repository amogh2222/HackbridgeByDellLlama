# ⚡ HackBridge — AI-Powered Hackathon Dashboard

<div align="center">

[![FastAPI](https://img.shields.io/badge/FastAPI-005571?style=for-the-badge&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com)
[![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)](https://react.dev)
[![Gemini](https://img.shields.io/badge/Google%20Gemini-8E75C2?style=for-the-badge&logo=googlegemini&logoColor=white)](https://ai.google.dev)
[![SQLite](https://img.shields.io/badge/SQLite-07405E?style=for-the-badge&logo=sqlite&logoColor=white)](https://sqlite.org)

**A unified hackathon management platform replacing fragmented coordination tools with a mathematically transparent API surface.**

</div>

---

## 🎯 Unique Selling Proposition (USP) & Differentiation
> [!IMPORTANT]
> **100% Explainable & Auditable Math:** Avoids "black-box" machine learning. Scoring, reviewer assignments, and group bias normalizations are calculated using transparent Z-scores and greedy multi-objective optimization, allowing organizers to trace and justify every result.
>
> **Demo-Resilient Fallback:** Combines Gemini AI skill extraction with a local regex-based fallback keyword parser. If external networks drop during judging, the application continues to run without interruptions.

---

## ⚙️ Tech Stack & Architecture
* **Core Application:** `FastAPI` (Async Python Backend) & `React` + `Vite` + `TypeScript` (Single-Page App).
* **Database & ORM:** `SQLite` powered by `SQLAlchemy` (Clean repository pattern).
* **Intelligence Engines:** `Google Gemini API` (Adaptive taxonomy tagging) & `RapidFuzz` (Fuzzy token-sort matching).

---

## 🚀 Core Features
* **🧠 Multi-Objective Reviewer Matcher:** greedy assignment engine optimizing for expertise (40%), workload (30%), conflict-of-interest exclusions (20%), and diversity (10%).
* **📊 Demographic Bias Normalization:** Flags statistical scoring gaps across gender, region, and institution using reviewer-level standard deviation adjustments.
* **🔍 Multi-Level duplicate flagger:** Detects exact email, fuzzy-name, and shared organization duplicates.
