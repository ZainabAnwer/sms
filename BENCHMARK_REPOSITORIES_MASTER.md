# Benchmark GitHub Repositories — Master Reference Guide

This document preserves the official GitHub repository URLs, technical stacks, module breakdowns, and architectural highlights extracted from our benchmarked repositories.

---

## 🏆 Top Recommended Repositories & Official Links

### 1. Coderbeb School Management System (Rank #1 — Enterprise Backend & Punctuality)
- **GitHub Repository**: [https://github.com/Coderbeb/School-Management-System](https://github.com/Coderbeb/School-Management-System)
- **Tech Stack**: Next.js 16 (App Router), PostgreSQL, Tailwind CSS v4, Radix UI.
- **Key Modules Extracted**:
  - Staff punctuality rules: `staff_entry_time` (08:00 AM), `staff_grace_minutes` (15 min), auto-late calculation, half-day detection.
  - Campus geofencing parameters (`geo_lat`, `geo_lng`, `geo_radius_meters`).
  - Automated PDF report cards via Puppeteer and official student certificates (Transfer Certificate, Character, Bonafide).

---

### 2. Maktab Academy Management System (Rank #2 — Attendance Kiosk & Bank Challans)
- **GitHub Repository**: [https://github.com/maktabtheeducationalinstitute-svg/academy-management-system](https://github.com/maktabtheeducationalinstitute-svg/academy-management-system)
- **Tech Stack**: React (Vite), TypeScript, Tailwind CSS, Supabase (PostgreSQL).
- **Key Modules Extracted**:
  - Dedicated **Attendance Kiosk Desk (`/attendance-desk`)**: Keyboard-wedge input for USB barcode / RFID / biometric scanner. Real-time student photo verification and audio chimes.
  - Red Fee Overdue warning banner on arrival scan.
  - Triplicate Bank Fee Challans (Bank Copy, School Copy, Student Copy) suited for Pakistani banks (Meezan / HBL).
  - Teacher course pacing planner (`course-breakdown`).

---

### 3. LavSMS (Rank #3 — BSEK Academic Marksheet & Promotion Engine)
- **GitHub Repository**: [https://github.com/4jean/lav_sms](https://github.com/4jean/lav_sms)
- **Tech Stack**: Laravel 8, Blade, MySQL.
- **Key Modules Extracted**:
  - Authentic terminal marksheet: Continuous Assessment (CA 40%) + Exam (60%).
  - Psychomotor and affective domain rating (1-5 scale for Punctuality, Neatness, Leadership).
  - Automated grade-to-grade student promotion engine and broadsheet master tabulation grid.
  - Result security PIN verification.
  - 7 user roles (Super Admin, Admin, Teacher, Student, Parent, Accountant, Librarian).

---

### 4. Hafizur Madrasa & School Management (Rank #4 — Biometric Machine Sync API)
- **GitHub Repository**: [https://github.com/HAFIZUR2004/madrasha-managment](https://github.com/HAFIZUR2004/madrasha-managment)
- **Tech Stack**: Next.js 15, TypeScript, Tailwind CSS, Firebase / MongoDB.
- **Key Modules Extracted**:
  - Real-time Biometric Machine Sync API webhook endpoint.
  - Live punch feed stream for gate logging.
  - Auto-SMS dispatch to parents on student absence.
  - QR-code enabled printable student and staff digital ID cards.

---

### 5. Upendra Dhamala SMS (Rank #5 — Non-Teaching Staff & Admit Cards)
- **GitHub Repository**: [https://github.com/upendradhamala/School-Management-System](https://github.com/upendradhamala/School-Management-System)
- **Tech Stack**: React, Express, MongoDB.
- **Key Modules Extracted**:
  - Dedicated **Non-Teaching Staff** module (drivers, security, lab attendants, caretakers) with dedicated payroll.
  - Official 110mm $\times$ 54.5mm printable examination admit cards with photo.
  - 6-part itemized fee breakdown (Tuition, Hostel, Lab, Computer, Exam, Misc).

---

### 6. ScholarOS
- **GitHub Repository**: [https://github.com/Harshit-Mudgal/ScholarOS](https://github.com/Harshit-Mudgal/ScholarOS)
- **Tech Stack**: Node.js, Express, PostgreSQL, React.
- **Key Highlights**: Clean 4-role hub (Admin, Teacher, Staff, Student) and assignments portal.

---

### 7. Yogndrr MERN SMS
- **GitHub Repository**: [https://github.com/Yogndrr/MERN-School-Management-System](https://github.com/Yogndrr/MERN-School-Management-System)
- **Tech Stack**: React, Express, MongoDB.
- **Key Highlights**: Baseline CRUD operations and simple attendance register.

---

### 8. Eskoofy SMS
- **GitHub Repository**: [https://github.com/hmjahid/school-management-system](https://github.com/hmjahid/school-management-system)
- **Tech Stack**: PHP / Laravel / Node.js.
- **Key Highlights**: Multi-stack reference architecture.

---

## 📌 Summary
All key architectural patterns, database schemas, and UX features from these repositories have been synthesized into our three core project documents:
- [01_SYSTEM_ARCHITECTURE_AND_TECH_STACK.md](file:///e:/MEEE/NORAI_WEBSITE_S/01_SYSTEM_ARCHITECTURE_AND_TECH_STACK.md)
- [02_MASTER_GOAL_AND_FULL_FEATURE_ROADMAP.md](file:///e:/MEEE/NORAI_WEBSITE_S/02_MASTER_GOAL_AND_FULL_FEATURE_ROADMAP.md)
- [03_CURRENT_STATUS_AND_PROTOTYPE_AUDIT.md](file:///e:/MEEE/NORAI_WEBSITE_S/03_CURRENT_STATUS_AND_PROTOTYPE_AUDIT.md)
- Live Prototype: [al_falah_grammar_school_showcase.html](file:///e:/MEEE/NORAI_WEBSITE_S/al_falah_grammar_school_showcase.html)
