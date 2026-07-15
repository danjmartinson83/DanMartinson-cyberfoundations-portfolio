# Week 2 — Student Submission Guide

**CyberFoundations · Tier I**

---

## Overview

Week 2 has one lab submission, committed to this repo:

```
week-02/
└── labs/
    └── lab-01-hardware-os-software-diagram.md
```

---

## Lab 01 — Hardware, OS, and Software Diagram

**Submission file:** `week-02/labs/lab-01-hardware-os-software-diagram.md`

**What to include:**

| Section | Requirement |
|---|---|
| Part A — District identification | District named, with your reasoning for why it fits |
| Part B, Step 1 — Layer examples | One specific example for hardware, OS, and software |
| Part B, Step 3 — Diagram | Embedded using a relative path, e.g. `../../assets/screenshots/week-02/diagram.png` |
| Part B, Step 4 — Explanation | Minimum 3 sentences, in your own words, referencing your own diagram |
| Analysis Questions (3) | Minimum sentence counts met for each |
| Lab Report Questions (3) | Answered in complete sentences |

**Format requirements:**
- Diagram embedded with a relative path — never an absolute path from your computer (e.g. `C:\Users\...` won't work for anyone but you)
- Explanations and analysis answers in your own words — not copied from the lesson
- Use the lab file's existing structure — don't delete sections

---

## Commit Instructions

**Commit message format:**
```
Week 2: <brief description>
```

Example:
- `Week 2: Hardware/OS/software diagram and analysis`

---

### Option 1 — GitHub Web UI

1. Go to your portfolio repository on GitHub.com
2. Navigate to `week-02/labs/`
3. Click on `lab-01-hardware-os-software-diagram.md`, then the pencil (edit) icon
4. Fill in your answers and embed your diagram
5. Scroll to **Commit changes**
6. Enter your commit message
7. Select **Commit directly to the main branch**
8. Click **Commit changes**

> To add your diagram image: go to `assets/screenshots/week-02/`, click **Add file → Upload files**, and upload your image there first — then reference it by filename in your lab file.

---

### Option 2 — VS Code

1. Open VS Code and open your portfolio repo folder
2. Save your diagram image into `assets/screenshots/week-02/`
3. Edit `week-02/labs/lab-01-hardware-os-software-diagram.md`
4. Open the **Source Control** panel (Ctrl+Shift+G / Cmd+Shift+G)
5. Stage your changes (click **+** next to **Changes**)
6. Enter your commit message
7. Click **✓ Commit**, then **Sync Changes** to push

---

### Option 3 — Git Commands

```bash
cd your-portfolio-repo
git add week-02/ assets/screenshots/week-02/
git commit -m "Week 2: Hardware/OS/software diagram and analysis"
git push
```

---

## Common Issues

| Issue | Fix |
|---|---|
| My diagram doesn't render on GitHub | Check your relative path — from `week-02/labs/lab-01-....md`, the path to your image is `../../assets/screenshots/week-02/filename.png` (two levels up, then into `assets/`). |
| I used an absolute path like `C:\Users\...` | That only works on your computer. Replace it with the relative path above. |
| I can't find the CyberFoundations City district | Revisit Week 1, Lesson 6 ("Welcome to CyberFoundations City") for the map. |
| My explanation feels too much like the lesson script | Rewrite it referencing your own diagram specifically — what does *your* diagram show, not what the lesson said in general. |

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
