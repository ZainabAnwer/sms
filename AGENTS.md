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

## 3. 🧠 Understand First, Confirm, Then Implement
- **Rule:** Jab bhi user koi naya kaam, requirement ya instruction bole:
  1. **Step 1:** Pehle apni **Understanding** wazeh lafzon mein bayan karni hai: *"Maine yeh kaam samjha hai ke: [Details]..."*
  2. **Step 2:** Plan aur approach brief mein batani hai.
  3. **Step 3:** Phir us kaam ko implement karna hai. Blindly assumptions par bina samjhe koi cheez nahi karni.

---

## 4. 🇵🇰 Target Context & Architecture
- **Target:** Pakistani Schools (BSEK Karachi board affiliated, K-10 / K-12).
- **Core Pillars:**
  - Role-Based Access Isolation (Super Admin vs Individual Teacher vs Student/Parent vs Accounts).
  - Triplicate Bank Challans (Meezan / HBL standard) + JazzCash/Easypaisa webhooks.
  - Hardware Biometric Engine (ZKTeco TCP/IP Port 4370) with 15m grace period and late-deduction rules.
  - Karachi BSEK Continuous Assessment (CA 40%) + Terminal Exam (60%) marksheets.
  - Sibling Concession, SheetJS bulk Excel onboarding, Transport fleet, and Digital Homework Diary.
