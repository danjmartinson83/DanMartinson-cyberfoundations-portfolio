# CyberFoundations — Week 11 Labs

## Module 4: Security Fundamentals & IAM
## Week 11: IAM & Active Directory — Who Gets Access to What?

This file is the **overview for the whole `week-11` folder**. It sits directly inside `week-11/`. It is different from `week-11/labs/README-week11-submissions.md`, which is the step-by-step upload and submission guide inside the `labs` folder.

This week you work in the **Cloud Heights Identity Center**, a browser-based learning environment that **simulates** Active Directory Domain Services (AD DS), Microsoft Entra ID and Azure resource access (RBAC). It is a safe practice copy — you are **not** administering real Microsoft systems, and nothing you do there affects any real organization.

## Sign In and How Your Work Is Saved

Week 11 uses the CyberFoundations Capstone site and **requires you to sign in** with either your username/email or your Google account.

Unlike the earlier weeks, Week 11 saves your IAM investigation, evidence, and Case File **under your individual student account**. This allows you to stop, return later, and continue where you left off.

Your work is saved separately from other students, and answer checks happen privately on the course side. Students do not see an answer key.

Use the **same account** for Week 11 and Week 12 so your Week 12 Communications Capstone can access the Week 11 Case File saved to your account.

[**Open Week 11 Capstone Lab**](https://capstone.cybervisionariesinstitute.org/cyberfoundations/week-11)

> **Why do Weeks 1–10 look different?** Earlier Capstone activities are open because they do not save individual student work inside the Capstone site. Weeks 11 and 12 use student-specific saved work, so sign-in is required.

## The Big Ideas (Explained Simply)

- **Person vs identity vs account:** a person is a human; an identity is how the system knows that person; an account is the login that identity uses. One person can have more than one account.
- **OU vs group vs role vs permission:** an **organizational unit (OU)** is a folder that organizes accounts; a **group** is a collection of accounts; a **role** is a named set of permissions; a **permission** is a single allowed action.
- **Authentication vs authorization:** authentication proves **who you are** (signing in); authorization decides **what you are allowed to do** after that.
- **Least privilege:** give each account only the access it needs to do its job — nothing more.
- **RBAC and ABAC:** role-based access control grants access by role; attribute-based access control grants access by attributes (like department or location).
- **AD DS vs Entra ID:** AD DS is the classic on-premises directory; Microsoft Entra ID is the cloud identity service. They solve similar problems in different places.
- **Joiner / Mover / Leaver:** the lifecycle of an account — created when someone joins, changed when they move roles, disabled when they leave.
- **Sign-in logs vs audit logs:** sign-in logs record authentication events; audit logs record what was changed or done.

## The Six Required Labs (In Order)

Complete all six labs in the **same persistent simulator state**. Do **not** reset between labs unless the mission instructions tell you to.

1. **Lab 01 — Identity Directory: Who Is Who?**
2. **Lab 02 — Authentication vs. Authorization**
3. **Lab 03 — Build and Manage the Directory**
4. **Lab 04 — Least Privilege Challenge**
5. **Lab 05 — Joiner, Mover, Leaver**
6. **Lab 06 — Identity Investigation + IAM Investigation Case File** — this produces your **Cloud Heights IAM Investigation Case File**, which is **Portfolio Deliverable 4**.

## Where Each Kind of Work Goes

| Place | What you do there |
|---|---|
| **Lab Portal** (this site) | Read the Lab 01–06 instruction guides, this overview and the submissions guide. Complete your Week 11 Notes and Reflection here. |
| **Cloud Heights Identity Center** — https://capstone.cybervisionariesinstitute.org/cyberfoundations/week-11 | Complete **all six interactive labs**. Follow the **Current Mission** instructions, capture evidence, and use **Download This Lab** / **Download & GitHub** to get your Markdown reports. |
| **Your own GitHub portfolio repository** | Store your six lab reports in `week-11/labs/` and your supporting Week 11 files. |
| **Lab Submission Tracker** — https://labsubmission.cybervisionariesinstitute.org | Paste the GitHub **file URL** for each lab submission. |

**Downloading is not submission.** Downloading a report does not upload it to GitHub, and uploading to GitHub does not record it in the tracker. Each step is separate.

## Lab 06 and Week 12

Lab 06 produces the **Cloud Heights IAM Investigation Case File (Portfolio Deliverable 4)**. Keep it safe: in **Week 12** you will use it as the source material for your **Technical Incident Report + Executive Summary**. Lab 06 is the only Deliverable 4 submission — there is no seventh report.

## Folder Map

| File | Purpose |
|---|---|
| `week-11/README-week11-root.md` | This overview |
| `week-11/labs/README-week11-submissions.md` | Upload and submission guide |
| `week-11/notes.md` | Your Week 11 notes (supporting) |
| `week-11/reflection.md` | Your Week 11 reflection (supporting) |
| `week-11/labs/lab-01-identity-directory.md` | Your Lab 01 report (required) |
| `week-11/labs/lab-02-authentication-vs-authorization.md` | Your Lab 02 report (required) |
| `week-11/labs/lab-03-build-and-manage-directory.md` | Your Lab 03 report (required) |
| `week-11/labs/lab-04-least-privilege-challenge.md` | Your Lab 04 report (required) |
| `week-11/labs/lab-05-joiner-mover-leaver.md` | Your Lab 05 report (required) |
| `week-11/labs/lab-06-identity-investigation-case-file.md` | Your Lab 06 case file (required, Deliverable 4) |
| Evidence folder from the complete ZIP | Supporting evidence captured by **Download & GitHub** |

From this file, open the [submissions guide](labs/README-week11-submissions.md), your [notes](notes.md), or your [reflection](reflection.md).

## Good to Know

- The simulator is persistent: your changes carry from lab to lab. Do not reset between labs unless instructed.
- Capture evidence as you go — it is much harder to recreate later.
- The six lab reports are the graded Week 11 deliverables recorded in the tracker.
- This overview, the submissions guide, your notes and your reflection are supporting portfolio resources. They add no new deadlines, no extra assessment and no extra tracker entries.
- If something looks wrong in the simulator, re-read the **Current Mission** panel first, then ask your instructor.

