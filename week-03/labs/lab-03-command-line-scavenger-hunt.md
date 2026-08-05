# Week 3 Lab 03 — Command Line Scavenger Hunt (CLI Simulator)

**Student Name:**  
**Date Completed:**  
**Module:** 1 — Digital Infrastructure & CLI | **Week:** 3
**Submission Path:** `week-03/labs/lab-03-command-line-scavenger-hunt.md`

---

## Overview

Labs 01 and 02 walked you through each command step by step. This lab is Week 3's wrap-up challenge: a deeper, more independent folder structure with three hidden files to track down, using the navigating and reading commands from Lessons 3A/3B, the creating and organizing commands from Lesson 3C, and your own judgment about when to ask for help. There's less hand-holding here on purpose — this is your chance to prove to yourself that the blinking cursor from the start of Lesson 3A doesn't intimidate you anymore.

**Nothing here can break anything real.** Same consequence-free CLI Simulator as Labs 01 and 02. Getting "lost" in the folder tree costs you nothing but a few extra `cd` moves.

---

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Environment | CyberFoundations CLI Simulator (browser-based, inside the Lab Portal) |
| Shell | Your choice — bash or PowerShell |
| Prerequisite | Labs 01 and 02 completed |

**Before you start:** log into the Lab Portal, open **Week 3 → CLI Simulator**, and load the **"Foundry District Archive Room"** scenario. This tree goes several folders deeper than Labs 01 and 02, and includes a few similarly-named folders on purpose — read carefully before you `cd` into anything.

---

## Part A — The Hunt

Find all three of the following, hidden at different depths in the Archive Room tree:

- A file related to a **shift log**
- A file related to a **maintenance note**
- A file related to a **supply inventory**

For each one, use `pwd`/`Get-Location` and `ls`/`dir` as many times as you need while you search, then record the **full path** once you find it.

Shift log file — full path once found:
```
(paste the full path here)
```
Maintenance note file — full path once found:
```
(paste the full path here)
```
Supply inventory file — full path once found:
```
(paste the full path here)
```

---

## Part B — Read and Report

For each of the three files you found in Part A, use `cat`/`type` to read it and record what it says.

Shift log contents:
```
(paste the file contents here)
```
Maintenance note contents:
```
(paste the file contents here)
```
Supply inventory contents:
```
(paste the file contents here)
```

---

## Part C — Organize Your Findings

Now that you've located and read all three files, clean up after yourself the way a professional would — don't leave your findings scattered across the tree.

### Step 1 — Create a Sorted-Findings Folder

Create a new folder called `sorted-findings` in your home directory.

Command you ran:
```
(paste the command here)
```

### Step 2 — Move All Three Files Into It

Move the shift log, maintenance note, and supply inventory files — the same three you found in Part A — into `sorted-findings`.

Commands you ran:
```
(paste the commands here)
```

### Step 3 — Confirm the Move

List the contents of `sorted-findings` to confirm all three files are now there.

Command you ran:
```
(paste the command here)
```
Output:
```
(paste the output here)
```

---

## Part D — When You Get Stuck

At some point in the Archive Room, you'll likely run across a command or folder name you don't immediately recognize.

### Step 1 — Ask the Terminal

When that happens, use `--help`, `man`, or `Get-Help` instead of guessing. Record what you looked up and what you learned.

Command or term you looked up:
```
(paste the command here)
```
What the help text (or the folder's contents) told you:
```
(describe it in your own words here)
```

### Step 2 — Describe a Wrong Turn

Everyone takes at least one wrong turn in a tree this size. Describe one moment you ended up somewhere unexpected, and how you used `pwd`/`Get-Location` and `cd ..` to recover.

```
(your answer here — minimum 2 sentences)
```

---

## Analysis Questions

### Analysis Question 1

Which of the three files in Part A took the longest to find, and what was it about the tree's structure (depth, similarly-named folders, etc.) that made it harder?

```
(your answer here — minimum 3 sentences)
```

### Analysis Question 2

Compare how you felt starting this lab to how you felt at the very start of Lesson 3A, looking at a blank blinking cursor for the first time. What changed?

```
(your answer here — minimum 3 sentences)
```

### Analysis Question 3

Week 4 moves from managing your own files to controlling who's allowed to do what to them — permissions — plus your first look at what a virtual machine is. Based on everything you've practiced this week, what's one thing you're curious about or looking forward to?

```
(your answer here — minimum 2 sentences)
```

---

## Submission Checklist

- [ ] All three target files located, with full paths recorded (Part A)
- [ ] All three target files read and their contents recorded (Part B)
- [ ] `sorted-findings` folder created and all three files moved into it, confirmed with a listing (Part C)
- [ ] At least one command or term looked up with `--help`/`man`/`Get-Help`, with what you learned recorded (Part D, Step 1)
- [ ] One wrong-turn moment described, including how you recovered (Part D, Step 2 — minimum 2 sentences)
- [ ] All three Analysis Questions answered (minimum sentence counts met)
- [ ] This file is committed to your portfolio repo at `week-03/labs/lab-03-command-line-scavenger-hunt.md`

---

## GitHub Commit Subsection

Same mechanism as Labs 01 and 02: fill out this lab's worksheet in the **CyberFoundations Lab Portal** (Week 3 → Lab 03) and click **Submit to GitHub** — the Portal commits the completed file to `week-03/labs/lab-03-command-line-scavenger-hunt.md` automatically. No manual typing or commit needed.

**📌 Optional:** a CLI Simulator session screenshot can be added the same way as Labs 01 and 02 — upload to `assets/screenshots/week-03/`, then right-click the uploaded image and choose **Copy image address**/**Copy Image Link** to embed it — but it isn't required and won't affect your grade.

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*

