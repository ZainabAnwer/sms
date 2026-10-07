# Al-Falah SchoolOS — Complete School Management System

> **Enterprise-grade, A-to-Z School Management System (SMS)** tailored for Pakistani educational institutions (BSEK Karachi board affiliated & private schools).

---

## 🏛️ System Overview

Al-Falah SchoolOS is a unified institutional operating system combining the best modules and architectures benchmarked from top production SMS systems (`Coderbeb`, `Maktab`, `LavSMS`, `Hafizur`, `Upendra`, `ScholarOS`).

### 🌟 Core Modules & Portals
- **👑 Super Admin (Principal Desk):** Complete school oversight, multi-faculty directory, admissions registry, fee master configuration, payroll, and audit logs.
- **👨‍🏫 Teacher Portal (Strict Individual Workspace):** Teacher schedule, assigned classes, subject grading, and class attendance registers with strict role isolation.
- **🎓 Student & Parent Portal:** Roll-number student dashboard, fee status, downloadable terminal report cards, and live attendance logs.
- **💰 Accounts & Bursar Desk:** Pakistani banking standard triplicate fee challans (Meezan / HBL Bank copy, Institution copy, Student copy), overdue fine engines, and collection ledgers.
- **⏱️ Hardware Biometric Engine:** Local LAN edge daemon (`pyzk`) connecting to ZKTeco / eSSL devices (Port 4370) for real-time punch ingestion, late arrival calculations, and grace periods.
- **📋 Academic Grading Engine:** Continuous Assessment (CA 40%) + Terminal Exam (60%) = BSEK Karachi board grades (A-1, A, B, C, D).

---

## 📚 Project Documentation

1. **[01_SYSTEM_ARCHITECTURE_AND_TECH_STACK.md](./01_SYSTEM_ARCHITECTURE_AND_TECH_STACK.md)**: Full system layers, Next.js 15+ App Router, Prisma ORM, PostgreSQL schema, and hardware daemon architecture.
2. **[02_MASTER_GOAL_AND_FULL_FEATURE_ROADMAP.md](./02_MASTER_GOAL_AND_FULL_FEATURE_ROADMAP.md)**: Master 0 to A-Z roadmap from Phase 1 (Prototype Verification) to Phase 5 (Production & Hardware Bridge).
3. **[03_CURRENT_STATUS_AND_PROTOTYPE_AUDIT.md](./03_CURRENT_STATUS_AND_PROTOTYPE_AUDIT.md)**: Current prototype audit, Pakistani seeded data inventory (25 students, 14 teachers), and credential isolation check.
4. **[BENCHMARK_REPOSITORIES_MASTER.md](./BENCHMARK_REPOSITORIES_MASTER.md)**: Curated list of all 8 benchmarked GitHub repositories, URLs, and architectural extracts.

---

## 🚀 Interactive Prototype Preview

The working interactive prototype is available in this repository:
- **Main Prototype File:** `al_falah_grammar_school_showcase.html`
- **Root Entrypoint:** `index.html`

To run locally:
```bash
python -m http.server 8080
```
Open `http://localhost:8080` in your browser.