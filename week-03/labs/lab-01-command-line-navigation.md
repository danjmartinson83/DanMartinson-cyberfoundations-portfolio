# Week 3 Lab — Navigate Your First File System (CLI Simulator)

**Student Name:** Dan Martinson

**Date Completed:** 8/8/2026

**Module:** 1 — Digital Infrastructure & CLI | **Week:** 3  
**Submission Path:** `week-03/labs/lab-01-command-line-navigation.md`

---

## Overview

Lesson 3 introduced your first five commands — finding where you are, looking around, moving through folders, peeking inside a file, and asking for help — in both bash and PowerShell. This lab has you apply those same five commands to a brand-new scenario inside the CLI Simulator, on your own, then connect what you find back to the file-system tree you learned to read in Lessons 1 and 2.

**Nothing here can break anything real.** The CLI Simulator is a consequence-free practice space — if you type something wrong, the worst outcome is an error message telling you so.

---

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Environment | CyberFoundations CLI Simulator (browser-based, inside the Lab Portal) — no install, no VM, no real terminal required |
| Shell | Your choice — bash or PowerShell. Try the same steps in both if you want extra practice; only one is required |
| Prerequisite | Lessons 1, 2, and 3 completed |

**Before you start:** log into the Lab Portal, open **Week 3 → CLI Simulator**, and load the **"Foundry District Shift Log"** scenario. This gives you a fresh, seeded set of folders and files you haven't seen before — that's intentional, so you're navigating for real, not just repeating the lesson's example.

---

## Part A — Find Your Way

### Step 1 — Open the Scenario and Check Your Starting Point

Load the Foundry District Shift Log scenario and run the command that tells you where you currently are (`pwd` in bash, `Get-Location` in PowerShell).

Command you ran:

```
morgan@foundry-wks2:/home/morgan$pwd
```

Output (your current path):

```
/home/morgan

```

### Step 2 — Look Around

Run the command that lists what's in your current location (`ls` in bash, `dir` in PowerShell).

Command you ran:

```
morgan@foundry-wk02:/home/morgan$ls
```

Output (files/folders listed):

```
README.md intake logs Maintenance
```

### Step 3 — Predict Before You Move

Before moving anywhere, look at the folder names from Step 2 and guess which one might contain a shift log or notes file. Write your guess down first — you'll check it in Part B.

My guess:

```
logs
```

---

## Part B — Move and Peek

### Step 1 — Move Into a Folder

Use `cd` (with a folder name from Step 2 as its argument) to move into the folder you guessed in Part A, Step 3.

Command you ran:

```
morgan@foundry-wk02:/home/morgan$cd logs
morgan@foundry-wk02:/home/morgan/logs$pwd
```

### Step 2 — Confirm Your New Location

Run `pwd` or `Get-Location` again to confirm exactly where you landed.

Command you ran:

```
morgan@foundry-wk02:/home/morgan/logs$pwd
```

Output (your new path):

```
/home/morgan/logs
```

### Step 3 — Look Around Again

Run `ls` or `dir` again in this new location. Keep moving with `cd` (repeating Steps 1–3 as needed) until you find a text file — something like a shift log, notes file, or README.

Command you ran:

```
morgan@foundry-wks-02:/home/morgan$cd logs
morgan@foundry-wks-02:/home/morgan/logs$ls
morgan@foundry-wks-02:/home/morgan/logs$ cat shift-log.txt
```

Output:

```
shift-log.txt
Shift log - Foundry District
06:00 - All systems normal.
14:00 - Routine inspection complete.
22:00 - Handoff to night shift.

```

### Step 4 — Peek Inside the File

Once you've found a text file, use `cat` (bash) or `type` (PowerShell) to read its contents.

Command you ran:

```
morgan@foundry-wks-02:/home/morgan$cd logs
morgan@foundry-wks-02:/home/morgan/logs$ls
morgan@foundry-wks-02:/home/morgan/logs$ cat shift-log.txt
```

File contents:

```
Shift log - Foundry District
06:00 - All systems normal.
14:00 - Routine inspection complete.
22:00 - Handoff to night shift.

```

### Step 5 — Move Back Up

Use `cd ..` at least once to move back up a level, and confirm with `pwd`/`Get-Location` that the path changed the way you expected.

Command you ran:

```
morgan@foundry-wks-02:/home/morgan/logs$cd ~
morgan@foundry-wks-02:/home/morgan/logs$cd ..
```

Output (confirming your new — higher — location):

```
morgan@foundry-wks-02:/home/morgan$
morgan@foundry-wks-02:/home/morgan$
```

---

## Part C — Ask for Help

### Step 1 — Pick an Unfamiliar Command

The CLI Simulator's Foundry District scenario includes one command you haven't been taught yet, shown as a hint in the scenario panel. Instead of guessing what it does, ask the terminal directly.

### Step 2 — Run the Help Command

Use `--help` or `man` (bash) or `Get-Help` (PowerShell) on that unfamiliar command.

Command you ran:

```
morgan@foundry-wks-02:/home/morgan$man grep
```

What the help text told you the command does, in your own words:

```
man grep searches inside files for a pattern. This is useful when a folder holds many files. 
```

---

## Analysis Questions

### Analysis Question 1

Look at the path `pwd` (or `Get-Location`) printed in Part A, Step 1. Is it written in Windows style or Linux style, and how do you know? Reference at least one specific detail from Lesson 2 (a drive letter, a slash direction, or the presence of a ~) to support your answer.

```
Linux uses / instead of \ which is used on Windows style.  When using the window peep to sneak a peek at what's inside a file user@foundry:~$cat notes.txt was used instead of typing out the entire address.  This works in finding the file faster to look at it. Also in Linux if you get lost and want to start over from home you can use morgan@foundry-wks-02:/home/morgan/logs$cd ~ or
morgan@foundry-wks-02:/home/morgan/logs$cd .. until you are home.
```

### Analysis Question 2

In Part B, you ran `pwd`/`Get-Location` right after moving with `cd`, more than once. Explain why that "move, then check" habit matters, especially while you're still building confidence with the command line.

```
It is important that after every move you make in the command line to check where you are and what's there.  It's using "The Golden Rule" for running commands. Before you move, look.  After you move, check where you are or what's there.
```

### Analysis Question 3

In Part C, you looked up a command you'd never used before, instead of guessing or skipping it. Explain why this habit — asking the terminal for help instead of memorizing everything in advance — matters for a real career in IT or cybersecurity.

```
Not a lot of people have every command that can be made memorized. Asking the terminal for help can help you acknowledge your location.  It can also help you see your next move or command.     
```

### Analysis Question 4

Compare this lab to Lesson 1's filing-room analogy (the pile of paper vs. the labeled cabinets). Now that you've actually navigated a file-system tree yourself instead of just reading about one, what — if anything — surprised you or felt different from what you expected?

```
When navigating the file system, it feels much more structured and organized.  Using a path hierarchy is much faster than searching on my own. Making work much more efficient. 
```

---

## Submission Checklist

- [x] Starting location recorded using `pwd`/`Get-Location` (Part A, Step 1)

- [x] Folder contents listed using `ls`/`dir` (Part A, Step 2)

- [x] Prediction written down before moving (Part A, Step 3)

- [x] Moved into a folder using `cd` and confirmed the new location with `pwd`/`Get-Location` **immediately after** the move, not just at the end (Part B, Steps 1–2)

- [x] Found and read a text file using `cat`/`type` (Part B, Steps 3–4)

- [x] Moved back up using `cd ..` and confirmed with `pwd`/`Get-Location` (Part B, Step 5)

- [x] Looked up an unfamiliar command using `--help`, `man`, or `Get-Help` and recorded what it does (Part C)

- [x] All four Analysis Questions answered (minimum sentence counts met)

- [x] This file is committed to your portfolio repo at `week-03/labs/lab-01-command-line-navigation.md`

---

## GitHub Commit Subsection

This lab's written answers are submitted the same way as Week 2's: through the **CyberFoundations Lab Portal**, not by typing directly into GitHub.

1. Go to the CyberFoundations Lab Portal and sign in with your student Microsoft account.
2. Open **Week 3 → Lab 01: Navigate Your First File System**.
3. Fill in the worksheet fields — they match the commands, outputs, and questions in this file.
4. Connect your GitHub account if you haven't already (one-time setup), and select your portfolio repo.
5. Click **Submit to GitHub**. The Portal commits the completed file to `week-03/labs/lab-01-command-line-navigation.md` for you — no manual typing or commit needed for this part.

**📌 Optional — add a screenshot for your portfolio.** This entire step is optional. Skipping it will **not** affect your grade — it's a nice-to-have addition to your portfolio, not a requirement. Only do this if you'd like a visual record of your CLI Simulator session.

If you'd like to add one, take a screenshot showing your commands and their output, then:

1. Go to your portfolio repository on GitHub.com and navigate to `assets/screenshots/week-03/`.
2. Click **Add file → Upload files**, drag in your screenshot, and give it a descriptive name (lowercase, hyphens, no spaces — e.g. `cli-simulator-session.png`).
3. Scroll down and click **Commit changes**.
4. Click on the uploaded image's filename to open it — you'll see the image itself displayed on the page.
5. Right-click directly on the image and choose **Copy image address** (Chrome/Edge) or **Copy Image Link** (Firefox).
6. Come back to this file, open the pencil (edit) icon, and add the embed near the bottom of Part B, pasting your copied link in place of the placeholder:

```markdown
![CLI Simulator session screenshot](paste your copied image link here)
```

**If right-click doesn't show that option** (e.g., on some trackpads or tablets): click the small download-arrow icon in the top-right of the image preview instead, then copy the URL from your browser's address bar.

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
