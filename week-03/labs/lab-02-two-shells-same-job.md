# Week 3 Lab 02 — Two Shells, Same Job: Incident Response Edition (CLI Simulator)

**Student Name:**  
**Date Completed:**  
**Module:** 1 — Digital Infrastructure & CLI | **Week:** 3
**Submission Path:** `week-03/labs/lab-02-two-shells-same-job.md`

---

## Overview

Welcome to your first Incident Response (IR) assignment in the **Foundry District Storeroom**. Our network monitoring system has flagged a potential unauthorized file access attempt on our storage systems, and you've been asked to investigate from two angles: first by connecting to a remote Linux database server (Pass A, in bash), then by sitting down at a Windows admin workstation examining that exact same shared storage (Pass B, in PowerShell). Your goal is to confirm the files look the same from both operating systems and that the directory tree matches — the same translation skill from Lesson 2, now applied to a real-feeling scenario instead of just a comparison slide. You'll also log your own findings along the way, using the create-and-organize commands from Lesson 3C — a real investigator never just looks and remembers, they document.

**Nothing here can break anything real.** Same consequence-free CLI Simulator as Lab 01.

---

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Environment | CyberFoundations CLI Simulator (browser-based, inside the Lab Portal) |
| Shells | Both bash **and** PowerShell are required — that's the whole point of this lab |
| Prerequisite | Lab 01 completed |

**Before you start:** log into the Lab Portal, open **Week 3 → CLI Simulator**, and load the **"Foundry District Storeroom"** scenario.

---

## 💡 Pro-Tips for Reducing Keyboard Strain

Before you start typing, remember these three professional efficiency "cheat codes":

- **Tab Completion (the autocomplete magic):** you don't need to type out long folder names — type the first few letters (e.g., `cd rep`) and press **Tab**. The shell will instantly autocomplete the folder name, in both bash and PowerShell.
- **Up Arrow (the recaller):** if you make a typo, don't retype the whole command — press the **Up Arrow** to recall your last command, use the left/right arrows to fix the typo, and hit **Enter**.
- **PowerShell aliases:** if typing `Get-Location` or `Get-ChildItem` feels too long, PowerShell lets you use `pwd` as a shortcut for location, and `ls` or `dir` for listing files.

---

## 🛠️ Lab Checklist

- [ ] Part A: Complete the Bash Pass (Linux), including creating and backing up your investigation note
- [ ] Part B: Complete the PowerShell Pass (Windows), including creating and backing up your investigation note
- [ ] Part C: Side-by-Side Comparison & Reflection
- [ ] Analysis Questions: Final Conceptual Review

---

## Part A — The Bash Pass (Linux Remote Server)

Connect to the **remote Linux terminal** in the CLI Simulator and execute the following investigative steps. Record your commands and output exactly as they appear.

### Step A1 — Verify Your Starting Location

Run the command to print your current working directory.

Command you ran:
```
(paste the command here)
```
Output:
```
(paste the output here)
```

### Step A2 — Look Around the Directory

List the contents of your current location to spot any files or folders.

Command you ran:
```
(paste the command here)
```
Output:
```
(paste the output here)
```

### Step A3 — Move Deeper into the Storeroom

Move into the `archive/incident-42` folder — flagged in the README as the one to investigate.

Command you ran:
```
(paste the command here)
```

**⚠️ Stop and check:** run your location-check command *immediately* after moving, to confirm you arrived safely.

Command you ran:
```
(paste the command here)
```
Output:
```
(paste the output here)
```

### Step A4 — Inspect the Incident Log File

Find a text file in this directory and print its contents to the screen to peek inside.

Command you ran:
```
(paste the command here)
```
Output:
```
(paste the output here)
```

### Step A5 — Create Your Investigation Note

Investigators document as they go. Create a new, empty file right here called `investigation-notes.txt` to hold your findings.

Command you ran:
```
(paste the command here)
```

### Step A6 — Back Up Your Note

Before you go any further, make a backup copy of `investigation-notes.txt` called `investigation-notes-backup.txt`, in case anything happens to your original.

Command you ran:
```
(paste the command here)
```

Confirm both files now exist:
```
(paste the output here)
```

---

## Part B — The PowerShell Pass (Windows Admin Workstation)

Now switch your simulator tab to **PowerShell**. You are examining the same shared storage room from a Windows administrative workstation. **You must target the exact same folder and file you used in Part A.**

### Step B1 — Verify Your Starting Location

Run the Windows command to print your current location.

Command you ran:
```
(paste the command here)
```
Output:
```
(paste the output here)
```

### Step B2 — Look Around the Directory

List the contents of your current location.

Command you ran:
```
(paste the command here)
```
Output:
```
(paste the output here)
```

### Step B3 — Move Deeper into the Storeroom

Move into `archive/incident-42` again — the same folder from Part A.

Command you ran:
```
(paste the command here)
```

**⚠️ Stop and check:** run your location-check command *immediately* after moving, to confirm you arrived safely.

Command you ran:
```
(paste the command here)
```
Output:
```
(paste the output here)
```

### Step B4 — Inspect the Incident Log File

Print the contents of the **exact same text file** you read in Part A.

Command you ran:
```
(paste the command here)
```
Output:
```
(paste the output here)
```

### Step B5 — Create Your Investigation Note

Create the **same-named** empty file, `investigation-notes.txt`, right here on the Windows side.

Command you ran:
```
(paste the command here)
```

### Step B6 — Back Up Your Note

Make a backup copy of `investigation-notes.txt` called `investigation-notes-backup.txt`, same as you did in Part A.

Command you ran:
```
(paste the command here)
```

Confirm both files now exist:
```
(paste the output here)
```

---

## Part C — Side-by-Side Comparison (Spot the Difference)

### Step C1 — The Command Comparison Table

Fill in the exact commands you typed for each task. Do not use generic names — list what you actually executed.

| Task / Question | Bash Command (Linux Pass) | PowerShell Command (Windows Pass) |
|---|---|---|
| 1. Where am I? | | |
| 2. Look around | | |
| 3. Move into a folder | | |
| 4. Peek inside a file | | |
| 5. Create + back up your note | | |

**⚠️ Stop and check:** did you use the exact same folder and file for both your bash and PowerShell passes? If they don't match, your comparison table below won't make sense — go back to Part B and re-target the same location before continuing.

### Step C2 — Output Differences Reflection

Describe at least one difference in how the two shells presented information to you (e.g., column layout, text colors, file details, folder headers). Minimum 2 sentences.

```
(your answer here)
```

---

## 🧠 Analysis Questions

### Analysis Question 1 — The Identical Tree

How do you know that the underlying file system tree was identical across both passes, even though you used completely different commands and operating systems? Point to concrete evidence from your terminal outputs (e.g., matching folder names, file content, or sizes). Minimum 3 sentences.

```
(your answer here)
```

### Analysis Question 2 — Syntax Preferences

Which command pair (e.g., pwd vs. Get-Location, ls vs. dir, cat vs. type) felt most different to you? Give a specific reason why one felt more comfortable or intuitive than the other. Minimum 3 sentences.

```
(your answer here)
```

### Analysis Question 3 — Applying Lesson 2 Differences

Describe how a specific difference you learned about in Lesson 2 (such as slash styles, case-sensitivity, or drive letters) was directly visible in your hands-on commands or output during this lab. Minimum 3 sentences.

```
(your answer here)
```

---

## Submission Checklist

- [ ] Part A completed entirely in bash (Steps A1–A6, all commands and output recorded)
- [ ] Location re-checked immediately after the Part A move (Step A3), not just at the end
- [ ] Investigation note created and backed up in Part A (Steps A5–A6)
- [ ] Part B completed entirely in PowerShell, on the same folder/file as Part A (Steps B1–B6)
- [ ] Location re-checked immediately after the Part B move (Step B3)
- [ ] Investigation note created and backed up in Part B, with the same filenames as Part A (Steps B5–B6)
- [ ] Comparison table filled in with actual commands, not placeholders (Part C, Step C1)
- [ ] Output-differences reflection written (Part C, Step C2 — minimum 2 sentences)
- [ ] All three Analysis Questions answered (minimum sentence counts met)
- [ ] This file is committed to your portfolio repo at `week-03/labs/lab-02-two-shells-same-job.md`

---

## GitHub Commit Subsection

Same mechanism as Lab 01: fill out this lab's worksheet in the **CyberFoundations Lab Portal** (Week 3 → Lab 02) and click **Submit to GitHub** — the Portal commits the completed file to `week-03/labs/lab-02-two-shells-same-job.md` automatically. No manual typing or commit needed.

**📌 Optional:** a CLI Simulator session screenshot can be added the same way as Lab 01 — upload to `assets/screenshots/week-03/`, then right-click the uploaded image and choose **Copy image address**/**Copy Image Link** to embed it — but it isn't required and won't affect your grade.

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*

