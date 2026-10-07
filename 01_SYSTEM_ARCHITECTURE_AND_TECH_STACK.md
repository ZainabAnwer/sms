# Al-Falah SchoolOS — System Architecture & Complete Tech Stack

This document specifies the complete, production-grade technical architecture, system layers, hardware integrations, and technology stacks for the **A-to-Z School Management System**.

---

## 1. High-Level Architectural Diagram

```
+---------------------------------------------------------------------------------------+
|                                    CLIENT CLIENTS                                     |
|  [Desktop Admin Hub]      [Teacher Tablet/Web]      [Student/Parent Web & Mobile PWA] |
+-------------------------------------------+-------------------------------------------+
                                            | HTTPS / WSS / JWT
+-------------------------------------------v-------------------------------------------+
|                          EDGE & REVERSE PROXY LAYER (Cloudflare)                      |
|                  DDoS Protection · SSL Termination · WAF · Tunnel Ingress              |
+-------------------------------------------+-------------------------------------------+
                                            |
+-------------------------------------------v-------------------------------------------+
|                          APPLICATION LAYER (Next.js 15+ / React 19)                   |
|  - App Router (/admin, /teacher, /student, /finance)                                  |
|  - Server Actions & Type-Safe API Route Handlers                                      |
|  - NextAuth / Lucia Auth (RBAC Middleware & Session Management)                        |
|  - PDF Generation Service (Triplicate Bank Challans, BSEK Report Cards)               |
+---------------------+-------------------------------+---------------------------------+
                      |                               |
       Database Queries (Prisma ORM)       Hardware Push/Webhook
                      |                               |
+---------------------v---------------+ +-------------v---------------------------------+
|     DATA LAYER (PostgreSQL 16)      | |      HARDWARE BIOMETRIC INTEGRATION ENGINE     |
| - Tenant Isolation (Campus / BSEK)  | | - Local LAN Edge Relay Daemon (Python/Node)   |
| - Users & Role Permissions (RBAC)   | | - ZKTeco / Realtime / eSSL Device SDK Socket  |
| - Students, Parents, Faculty Tables | | - RFID Gate Card Readers & Fingerprint Scans   |
| - Attendance Logs with Timestamps   | | - Real-time Clock-In / Clock-Out Ingestion     |
| - Finance, Ledgers & Challan Records| +-----------------------------------------------+
| - Marksheets & BSEK Grade Tables    |
+-------------------------------------+
```

---

## 2. Technology Stack Selection & Specifications

### 2.1 Frontend & User Experience (UX) Stack
| Component | Technology | Rationale & Enterprise Justification |
| :--- | :--- | :--- |
| **Framework** | **Next.js 15+ (App Router)** | Industry gold standard for production web apps. Hybrid SSR/SSG ensures instant page loads, SEO for public school portals, and secure Server Components. |
| **Language** | **TypeScript (Strict Mode)** | End-to-end type safety across database schemas, API payloads, and portal interfaces to eliminate runtime errors. |
| **Styling** | **Tailwind CSS + CSS Modules** | Zero-runtime CSS, ultra-fast rendering, responsive across mobile, tablets, and high-res administrative displays. |
| **UI Component Library** | **Shadcn UI + Radix UI Primitives** | Unstyled accessible primitives, fully customizable, zero vendor lock-in. |
| **Icons & Media** | **Lucide Icons + FontAwesome 6 Pro** | Crisp, comprehensive iconography for administrative controls, academic subjects, and financial statuses. |
| **Data Tables** | **TanStack Table v8** | Virtualized row rendering for 1000+ student rosters with column filtering, multi-sort, and CSV/Excel exports. |
| **Charts & Analytics** | **Recharts / Tremor** | Beautiful visual KPI dashboards for attendance punctuality, fee collection curves, and student GPA trends. |
| **Printing & PDF** | **@react-pdf/renderer + Browser Print CSS** | Generates pixel-perfect 3-part bank challans (Bank/School/Student copies) and BSEK-compliant terminal marksheets. |

---

### 2.2 Backend & Application Layer Stack
| Component | Technology | Rationale & Enterprise Justification |
| :--- | :--- | :--- |
| **Runtime** | **Node.js 22 LTS / Bun** | High-performance asynchronous execution for handling hundreds of concurrent roll-call entries and ledger operations. |
| **API Architecture** | **Next.js Server Actions + REST APIs** | Zero-boilerplate server-side data fetching and mutation with automatic cache invalidation and CSRF protection. |
| **Validation** | **Zod v3** | Strict schema validation on all client submissions (admissions, marks entry, fee adjustments). |
| **Authentication & RBAC** | **NextAuth.js (Auth.js) / Supabase Auth** | Multi-role credential authentication (Email/Username/Roll No + Password), bcrypt password hashing, and encrypted JWT tokens. |
| **Background Jobs** | **BullMQ + Redis / Inngest** | Asynchronous queuing for bulk SMS notifications, monthly fee challan generation, and nightly database backups. |

---

### 2.3 Database & Storage Layer
| Component | Technology | Rationale & Enterprise Justification |
| :--- | :--- | :--- |
| **Primary Database** | **PostgreSQL 16** | Robust relational database with ACID guarantees, essential for school financial ledgers and academic grading integrity. |
| **ORM / Query Builder** | **Prisma ORM** | Type-safe migrations, auto-generated TypeScript clients, and intuitive relational querying across students, classes, and teachers. |
| **Caching & In-Memory Store** | **Redis 7** | Sub-millisecond caching for master timetables, active session tokens, and hardware attendance rate-limiting. |
| **File & Asset Storage** | **Cloudflare R2 / AWS S3** | Secure, zero-egress fee object storage for student admission photos, CNIC/B-Form scans, teacher qualifications, and circular PDFs. |

---

### 2.4 Hardware & Biometric Attendance Integration Stack

School management systems in Pakistan require bulletproof teacher and student attendance tracking that prevents proxy sign-ins.

```
+------------------------------------+
|  Biometric Terminal (On Campus)    |
|  (e.g., ZKTeco K40 / VF380 / MB20) |
+-----------------+------------------+
                  | TCP/IP (Local School LAN)
+-----------------v------------------+
| Local Hardware Daemon (Edge Relay) |
| - Runs on Admin PC (Python / Go)   |
| - Pulls punches via pyzk / SDK     |
+-----------------+------------------+
                  | HTTPS REST Webhook / Encrypted API Key
+-----------------v------------------+
| Cloud Backend Attendance Ingestion |
| - Validates Machine ID & Timestamp |
| - Computes Punctuality & Grace Min |
| - Updates Teacher/Student Database |
+------------------------------------+
```

* **Device Protocols:** ZKTeco Standalone SDK / pyzk (Python ZK Library) over TCP/IP Port 4370.
* **Edge Ingestion Daemon:** A lightweight local service installed on the school's local administrative PC. It continuously listens for biometric machine events (fingerprint scan, face recognition, RFID card tap).
* **Clock-in / Clock-out Logic:**
  * **Teacher Rules:** Grace period until 08:00 AM. Arrival between 08:00–08:15 AM marked "Late". 3 Late arrivals = 1/2 day salary deduction rule.
  * **Student Rules:** Gate closes at 08:00 AM. Fingerprint tap records gate arrival timestamp. Trigger automated SMS/WhatsApp notification to guardian if absent by 08:30 AM.

---

## 3. Core Database Models & Relationships

```mermaid
erDiagram
    SCHOOL ||--o{ ACADEMIC_YEAR : has
    SCHOOL ||--o{ USER : employs_or_enrolls
    SCHOOL ||--o{ CLASS_SECTION : organizes
    
    USER ||--o| TEACHER_PROFILE : has
    USER ||--o| STUDENT_PROFILE : has
    USER ||--o| GUARDIAN_PROFILE : has
    
    CLASS_SECTION ||--o{ STUDENT_PROFILE : contains
    CLASS_SECTION ||--o{ SUBJECT : offers
    TEACHER_PROFILE ||--o{ CLASS_SECTION : class_incharge
    
    SUBJECT ||--o{ TEACHER_PROFILE : taught_by
    STUDENT_PROFILE ||--o{ ATTENDANCE_RECORD : logs
    TEACHER_PROFILE ||--o{ ATTENDANCE_RECORD : logs
    
    STUDENT_PROFILE ||--o{ FEE_CHALLAN : billed
    FEE_CHALLAN ||--o{ FEE_TRANSACTION : pays
    
    STUDENT_PROFILE ||--o{ EXAM_MARKS : receives
    SUBJECT ||--o{ EXAM_MARKS : grades
```

### 3.1 Primary Database Tables:
1. `users` (id, school_id, email, username, password_hash, role [SUPER_ADMIN, TEACHER, STUDENT, ACCOUNTANT, GUARDIAN], status, created_at)
2. `teachers` (id, user_id, employee_id, full_name, qualification, designation, basic_salary, joined_date, phone, incharge_class_id)
3. `students` (id, user_id, roll_number, b_form_number, full_name, father_name, guardian_phone, current_class_id, admission_date, status)
4. `class_sections` (id, name, numeric_level [Nursery..10], stream [Science, General], class_teacher_id)
5. `subjects` (id, name, code, class_id, primary_teacher_id, weekly_periods)
6. `attendance_logs` (id, user_id, role, date, clock_in_time, clock_out_time, status [PRESENT, LATE, ABSENT, LEAVE], source [BIOMETRIC, MANUAL_PORTAL])
7. `fee_challans` (id, student_id, month, year, tuition_fee, lab_fee, arrears, total_amount, due_date, status [UNPAID, PAID, OVERDUE], bank_ref)
8. `exam_results` (id, student_id, subject_id, term [MIDTERM, FINAL], ca_score_40, terminal_score_60, total_marks, grade, gpa)

---

## 4. Role-Based Access Control (RBAC) Permission Matrix

| Module / Operation | Super Admin | Teacher | Student / Parent | Accountant |
| :--- | :---: | :---: | :---: | :---: |
| **All Teachers Directory & Salaries** | Full (CRUD) | ❌ Denied | ❌ Denied | Read/Payroll Only |
| **My Personal Teacher Workspace** | Full (Inspect) | Own Profile Only | ❌ Denied | ❌ Denied |
| **All Students Directory (All Classes)** | Full (CRUD) | ❌ Denied | ❌ Denied | Read Only |
| **My Assigned Class Students** | Full (CRUD) | Own Classes (Read/CA) | ❌ Denied | ❌ Denied |
| **Daily Attendance Register** | School-wide | Own Incharge Class | ❌ Denied | ❌ Denied |
| **My Personal Attendance / Report** | Full (All) | Own Log Only | Own Log Only | ❌ Denied |
| **Marks Entry & Exam Grading** | Final Lock | Own Subject Entry | ❌ Denied | ❌ Denied |
| **Fee Challan Generation & Ledger** | Full Oversight | ❌ Denied | Own Challan View/Print | Full (CRUD & Collect) |
| **Official Circulars & Notices** | Publish/Delete | Read Staff Notices | Read Student Notices | Read Finance Notices |
| **Hardware & Biometric Ingestion** | Full Config | Read Own Clock-in | Read Own Arrival | ❌ Denied |

---

## 5. Security & Compliance Architecture

1. **Password Security:** Salted `bcrypt` hashing with work factor 12.
2. **Session Security:** HTTP-Only, Secure, SameSite cookies with short-lived JWTs and Redis-backed refresh token rotation.
3. **Data Protection:** Database connection over TLS with SSL certificate enforcement; daily automated snapshot backups stored off-site.
4. **Audit Logs:** Immutable audit log table recording every financial transaction, mark alteration, and administrative privilege escalation.
