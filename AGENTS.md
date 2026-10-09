# Project Memory & Operating Rules (Al-Falah SchoolOS / SMS)

These rules are permanently active for this project and must be strictly followed on every prompt:

---

## 1. 🔄 State File Must Be Updated After Every Prompt
- **Target File:** [`03_CURRENT_STATUS_AND_PROTOTYPE_AUDIT.md`](./03_CURRENT_STATUS_AND_PROTOTYPE_AUDIT.md)
- **Rule:** Har prompt / task / milestone complete hone ke baad `03_CURRENT_STATUS_AND_PROTOTYPE_AUDIT.md` ko update karna LAZMI hai (bhale short bullet points mein ho).
- **Purpose:** Current status, completed work, aur next pending steps hamesha ek central file mein up-to-date rahenge.

---

## 2. 🚫 Strict No Git Push / Commit Without Explicit Permission
- **Rule:** GitHub repository par `git push` ya `git commit` hargiz nahi karna jab tak USER saaf lafzon mein push karne ki permission na de ya explicitly "push karo" na bole.
- **Work Mode:** Local changes, local code editing, aur local testing dev server par hi honge. Push sirf user ki ijazat par hoga.

---

## 3. 🧠 Understand First, Confirm, Then Implement (Calibrated by Task Size)
- **Rule:**
  - **Chote / Routine Tasks (e.g. push, status, quick edits):** Sirf **1 line** mein concise confirmation de kar tokens / credits bachane hain. Lambi boilerplate details repeat nahi karni.
  - **Bare Coding / New Feature Tasks:** Pehle apni **Understanding** wazeh bayan karni hai, plan aur approach batani hai, phir implementation karni hai.

---

## 4. 🇵🇰 Target Context & Architecture
- **Target:** Pakistani Schools (BSEK Karachi board affiliated, K-10 / K-12).
- **Core Pillars:**
  - Role-Based Access Isolation (Super Admin vs Individual Teacher vs Student/Parent vs Accounts).
  - Triplicate Bank Challans (Meezan / HBL standard) + JazzCash/Easypaisa webhooks.
  - Dual Attendance Engine: Hardware (ZKTeco TCP/IP 4370) + Zero-Hardware Mobile Geofence (<50m) + WebAuthn Fingerprint.
  - Karachi BSEK Continuous Assessment (CA 40%) + Terminal Exam (60%) marksheets.
  - Sibling Concession, SheetJS bulk Excel onboarding, Transport fleet, and Digital Homework Diary.
