# Week 4 Lab — The Archive Investigation (CLI Simulator)

**Student Name:** Dan Martinson

**Date Completed:** 8/10/2026

**Module:** 1 — Digital Infrastructure & CLI | **Week:** 4  
**Submission Path:** `week-04/labs/lab-02-wildcards-and-searching.md`

---

## Overview

Lesson 2 gave you the Archive's two tools: patterns that match many filenames at once, and the magnet — `grep` — that searches *inside* files. This lab hands you an Archive of your own and a request slip with three jobs on it: match a set of files with patterns (Part A), hunt down a suspicious log entry with grep (Part B), and run the full find → check → lock down audit that combines this week's two lessons into one workflow (Part C). This lab is more independent than Lab 01 — like Week 3's Scavenger Hunt, the steps tell you *what* to accomplish, and the *how* is on you. One screenshot from this lab becomes part of ★ Deliverable 1.

---

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Environment | CyberFoundations CLI Simulator (browser-based, inside the Lab Portal) |
| Shell | Your choice — bash or PowerShell. The steps below show bash syntax; the Lesson 2 Resource Pack's Quick Reference has the PowerShell equivalents |
| Prerequisite | Week 4, Lessons 1 and 2 completed; Lab 01 recommended first |

**Before you start:** log into the Lab Portal, open **Week 4 → CLI Simulator**, and load the **"Foundry District Archive Investigation"** scenario. It seeds a folder of several dozen files — logs, invoices, notes — far too many to open one at a time. Good.

---

## Part A — Work the Request Slip

### Step 1 — Survey the Archive

Before filtering anything, look at what you're working with: run a plain listing of the Archive folder. You don't need to record every filename — just note roughly how many files there are and what naming families you can see (invoices, logs, notes…).

What you observed (rough count + the naming families you spotted):

```
3 access.logs
5 invoice.txts
1 notes.txt
1 meeting recap.txt
```

### Step 2 — Match One Family With a Pattern

The slip's first request: **every invoice file.** Write a pattern that matches all of them and *only* them, and test it with `ls` — remember the habit: pattern first, look at what it catches, then act.

Command you ran (your ls + pattern):

```
morgan@foundry:/home/morgan/archive$ ls inv*
```

Output (the matched files):

```
inv-april.txt
inv-february.txt
inv-january.txt
inv-march-supplement.txt
inv-march.txt
```

### Step 3 — Get Precise

The slip gets pickier: **only the invoices from a single month** (the scenario panel tells you which). Refine your pattern so it catches exactly those — you may need a second `*`, a `?`, or a `[ ]` set, depending on how the names are built.

Command you ran:

```
ls inv-march*
```

Output (the matched files — and nothing extra):

```
inv-march-supplement.txt
inv-march.txt
```

### Step 4 — Act on a Pattern

Create a folder named `evidence` and copy your Step 3 matches into it with a single `cp` command using your pattern. Confirm the copies landed with `ls evidence`.

Commands you ran (mkdir, cp with pattern, confirming ls):

```
morgan@foundry:/home/morgan/archive$ mkdir evidence
morgan@foundry:/home/morgan/archive$ cp inv-march* evidence
morgan@foundry:/home/morgan/archive$ ls
door-access.log  east-access.log  evidence  inv-april.txt  inv-february.txt  inv-january.txt  inv-march-supplement.txt  inv-march.txt  meeting-recap.txt  notes-march-meeting.txt  supply-list.txt  west-access.log
morgan@foundry:/home/morgan/archive$ cd evidence
morgan@foundry:/home/morgan/archive/evidence$ ls
inv-march-supplement.txt  inv-march.txt
morgan@foundry:/home/morgan/archive/evidence$

```

---

## Part B — Run the Magnet

### Step 1 — Search One File

The slip's second request: the scenario's access log records badge events, and somewhere in it are **denied entries**. Search the log the scenario panel names for the word `denied` — and remember the Strict Teacher: decide whether you need the case-insensitive flag.

Command you ran:

```
morgan@foundry:/home/morgan/archive$  grep -i denied *.log
```

Output (every matching line):

```
morgan@foundry:/home/morgan/archive$  grep -i denied *.log
door-access.log:08:12 DENIED badge 2214 east door - retry OK
door-access.log:12:40 DENIED visitor badge front desk
door-access.log:02:47 DENIED badge 4471 storeroom door
west-access.log:13:22 DENIED badge 9911 west door - unknown badge
```

### Step 2 — Find the Line That Matters

Most denied entries are routine — mistyped badges at reasonable hours. One is not. Identify the suspicious line (think: what *time* would worry you?) and record it exactly.

The suspicious line, and why you flagged it:

```
door-access.log:02:47 DENIED badge 4471 storeroom door       It's 2:47AM not business hours
```

### Step 3 — Widen the Sweep

One log is never the whole story. Re-run your search across **every** log file in one command — a pattern where the filename goes. Note which files your suspicious word appears in.

Command you ran:

```
morgan@foundry:/home/morgan/archive$ grep -i badge-code *.txt

```

Which files contained matches:

```
meeting-recap.txt:Action: rotate the storeroom badge-code list this quarter
```

---

## Part C — Find, Check, Lock Down

The slip's last request is the real test: **somewhere in this Archive is a file listing storeroom badge codes.** You don't know its name. You know what's inside it.

### Step 1 — Find It by Its Contents

Search every text file for the term the scenario panel gives you, in one command. Record which file comes back.

Command you ran:

```
morgan@foundry:/home/morgan/archive$ cat door-access.log -i
```

The file you found:

```
morgan@foundry:/home/morgan/archive$ cat door-access.log -i
07:58 GRANTED badge 2214 east door
08:12 DENIED badge 2214 east door - retry OK
09:31 GRANTED badge 4471 west door
12:40 DENIED visitor badge front desk
17:05 GRANTED badge 8832 north door
02:47 DENIED badge 4471 storeroom door
06:01 GRANTED badge 2214 east door

```

### Step 2 — Check Who Can Touch It

Before you walk away — this is the Week 4 reflex now — run the long listing on that file and read its rings. Record what you find. Is this file as locked down as its contents deserve?

Command you ran and its output:

```
ls -l
-rw-r--r-- 1 morgan foundry   262 door-access.log
-rw-r--r-- 1 morgan foundry    69 east-access.log
-rw-r--r-- 1 morgan foundry    36 inv-april.txt
-rw-r--r-- 1 morgan foundry    41 inv-february.txt
-rw-r--r-- 1 morgan foundry    43 inv-january.txt
-rw-r--r-- 1 morgan foundry    49 inv-march-supplement.txt
-rw-r--r-- 1 morgan foundry    38 inv-march.txt
-rw-rw-rw- 1 morgan foundry   129 meeting-recap.txt
-rw-r--r-- 1 morgan foundry    70 notes-march-meeting.txt
-rw-r--r-- 1 morgan foundry    49 supply-list.txt
-rw-r--r-- 1 morgan foundry   119 west-access.log
```

Your read of the situation:

```
If everyone can read and write meeting-recap.txt, anyone can write an excuse to be there in the middle of the night.
```

### Step 3 — Lock It Down

Fix the file's permissions so only its owner can read and write it — Gatekeeper's Rule applies: check, change, check again.

Commands you ran (including both ls -l checks):

```
morgan@foundry:/home/morgan/archive$ ls -l
morgan@foundry:/home/morgan/archive$ chmod g-rw meeting-recap.txt
morgan@foundry:/home/morgan/archive$ ls -l
morgan@foundry:/home/morgan/archive$ chmod o-rw meeting-recap.txt
morgan@foundry:/home/morgan/archive$ ls -l
```

The file's permission string BEFORE and AFTER:

```
-rw-rw-rw- 1 morgan foundry   129 meeting-recap.txt        (Before)
-rw------- 1 morgan foundry   129 meeting-recap.txt        (After)  
```

### Step 4 — Capture Your Investigation Evidence (REQUIRED screenshot)

Take one screenshot of your simulator session showing your Part C sequence — the search that found the file, the permission check, and the fix. **This screenshot is required — it is part of ★ Deliverable 1.** Name it `cli-search-investigation.png`. Upload and embed it via the GitHub Commit section below.

---

## Analysis Questions

**Analysis Question 1.** In Part A you tested every pattern with `ls` before letting `cp` act on it. Explain what could go wrong if you skipped straight to acting — and why the stakes get higher when the command attached to the pattern is `rm`. *(Minimum 2 sentences.)*

```
ls looks at the files and items.
cp is just making a copy of an item.
rm remove data is gone unless it's backed up forever; much higher stakes 
```

**Analysis Question 2.** Your Part B search returned several routine matches and one suspicious one. In a real security job, why is "reducing six hundred lines to three worth reading" often more valuable than any single answer the search returns? *(Minimum 2 sentences.)*

```
In security, getting the hard facts fast is important. Looking through six hundred lines to find those three would have taken forever.  Finding the problem fast.  Find, identify, and neutralize the threat.
```

**Analysis Question 3.** Part C found a sensitive file by its *contents*, then audited its *permissions*. Explain why neither skill alone would have been enough — what does each half of the workflow catch that the other misses? *(Minimum 3 sentences.)*

```
Finding the sensitive file by its contents was important.  It was sensitive information in the wrong place. That file had way too many permissions for the information it contained. Both of the issues needed to be fixed and reorganized, not just audited for permissions. 
```

**Analysis Question 4.** The Archive had dozens of files; real systems have millions. Which habit from this lab do you think scales up the furthest into professional work, and why? *(Minimum 2 sentences.)*

```
The use of grep in order to find what you were looking for and its location scales up to professional work the most. I am learning on a smaller scale when in the real world it could be much larger.
```

---

## Submission Checklist

- [x] Archive surveyed and naming families noted (Part A, Step 1)

- [x] Full invoice family matched with a tested pattern (Part A, Step 2)

- [x] Precise single-month pattern built and verified (Part A, Step 3)

- [x] Matches copied to `evidence/` with one pattern-driven `cp` (Part A, Step 4)

- [x] Log searched for denied entries with correct case handling (Part B, Step 1)

- [x] Suspicious line identified with reasoning (Part B, Step 2)

- [x] Multi-file sweep run in one command (Part B, Step 3)

- [x] Hidden file found by contents (Part C, Step 1)

- [x] Its permissions checked and assessed (Part C, Step 2)

- [x] Locked down to owner-only with before/after checks (Part C, Step 3)

- [x] **REQUIRED:** `cli-search-investigation.png` uploaded to `assets/screenshots/week-04/` and embedded below (Part C, Step 4)

- [x] All four Analysis Questions answered (minimum sentence counts met)

- [x] This file is committed to your portfolio repo at `week-04/labs/lab-02-wildcards-and-searching.md`

---

## GitHub Commit Subsection

This lab's written answers are submitted through the **CyberFoundations Lab Portal**.

1. Go to the CyberFoundations Lab Portal and sign in.
2. Open **Week 4 → Lab 02: The Archive Investigation**.
3. Fill in the worksheet fields — they match the commands, outputs, and questions in this file.
4. Click **Submit to GitHub**. The Portal commits the completed file to `week-04/labs/lab-02-wildcards-and-searching.md` for you.

**📸 REQUIRED — your Deliverable 1 screenshot.**

1. On GitHub.com, navigate to your portfolio repo's `assets/screenshots/week-04/` folder.
2. Click **Add file → Upload files**, drag in your screenshot named `cli-search-investigation.png` (lowercase, hyphens, no spaces), and click **Commit changes**.
3. Click the uploaded image's filename to open it, then right-click directly on the image and choose **Copy image address** (Chrome/Edge) or **Copy Image Link** (Firefox).
4. Edit this lab file and paste your copied link into the embed below, at the end of Part C:

**If right-click doesn't show that option:** click the small download-arrow icon in the top-right of the image preview instead, then copy the URL from your browser's address bar.

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
