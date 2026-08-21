# Week 6 Lab 01 — Claiming Your Room in Cloud Heights

**Student Name:** Dan Martinson

**Date Completed:** 8/21/2026

**Module:** 2 — Networking & Cloud Foundations | **Week:** 6  
**Submission Path:** `week-06/labs/lab-01-claiming-your-room.md`

---

> ### 🔒 Cloud Heights Security Rule
> Your Bastion link and Cloud Heights password are **private access credentials**. Never paste either into a worksheet, screenshot, GitHub repository, Circle post, or chat message. When taking screenshots, crop out the browser address bar and all login information.

---

## Overview

Week 5 was practice. This week the machine is real. Cloud Heights is a live Ubuntu 22.04 server running in Azure, and one of its rooms has **already been reserved for you** — you do not create it, provision it, or pay for it. Your job in this lab is to walk in the front door, prove you are standing inside your own room, and understand where that room came from.

This is a **guided** lab. Every step tells you what to do and what to record. Expect 30–40 minutes.

---

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Environment | Cloud Heights — live Ubuntu 22.04 VM in Azure, reached through Azure Bastion in your browser |
| Access | Lab Portal → **My Lab Environment** → your Cloud Heights card |
| Username | `analyst` |
| Password | Provided to you separately. Never typed into this worksheet. |
| Commands used | `hostname`, `whoami`, `pwd` |
| Auto-shutdown | Your VM stops automatically after 15 minutes of inactivity. A warning with **Keep Working** appears first. |

**Before you start:** open **My Lab Environment** in the Portal. If your VM shows **Stopped**, click **Start VM** and wait until the status reads **Running** — this takes a minute or two. Only then click **Open Cloud Heights**.

---

## Part A — Walking In

### Step 1 — Start the Room

In **My Lab Environment**, check your Cloud Heights status. Start the VM if it is stopped and wait for **Running**.

The status you saw before you started, and the status you saw after:

```
Start VM with play symbol
after click 
Open cloud heights and a stop VM button next to it
```

### Step 2 — Open Cloud Heights and Sign In

Click **Open Cloud Heights**. A browser-based session opens through Azure Bastion. Sign in with username `analyst` and the password you were given separately.

**Do not record the password, the link, or any part of the login screen anywhere.**

Describe what you saw once the session opened — what kind of screen greeted you:

```
AZURE BASTION ASKING FOR 
PROTOCOL
PORT
Authentication Type
Username
Password
```

### Step 3 — Ask the Machine Its Name

Run:
```
hostname
```
Output:

```
cf-student -07
```

### Step 4 — Ask Who You Are

Run:
```
whoami
```
Output:

```
analyst
```

### Step 5 — Ask Where You Are Standing

Run:
```
pwd
```
Output:

```
/home/analyst
```

---

## Part B — What Those Three Answers Prove

### Step 1 — Read Them as Evidence

Each of those three commands answered a different question: *which machine*, *which identity*, *which location in the filesystem*. Together they are the proof that you are inside your own room and not somebody else's.

Explain, in your own words, what each output proves:

```
Running hostname returned cf-student-07, which proves you are connected to your designated Virtual Machine rather than another student's server. Executing whoami output analyst, verifying that you are logged in under your specific assigned user account. Finally, pwd displayed /home/analyst, confirming you are currently positioned in your personal user directory within the filesystem. Together, these outputs confirm your machine identity, user identity, and filesystem location. A good start.
```

### Step 2 — Capture Your Evidence

Take a screenshot of your terminal showing the three commands and their outputs.

**Required filename:** `bastion-session.png`

**Crop rules — not optional.** The screenshot must show the terminal and prompt. It must **not** show the browser address bar, the Bastion link, any login screen, or any password field. Crop before you upload.

Upload it to `assets/screenshots/week-06/` in your portfolio repository, then paste its link here:

---

## Part C — Where Your Room Came From

### Step 1 — The Golden Image Idea

Every student's Cloud Heights room was built from the **same standardized image** — a known-good snapshot of a configured Ubuntu machine. Nobody hand-built 20 servers. One machine was configured correctly once, captured, and stamped out repeatedly.

Explain in your own words what a standardized (golden) image is and why an organization would build one:

```
Think of a golden image like a master cookie cutter. Instead of shaping and decorating every single cookie by hand from scratch, you make one perfect template and use it to cut out identical cookies super fast.

A golden image is a single pre-made setup of a computer—with the operating system, programs, and security settings already installed and tuned to perfection.

Organizations build a golden image for a few simple reasons

Using a golden image means setting up one master computer takes a little time, but copying it onto 100 new computers takes just minutes instead of days.

Golden images prevent mistakes. Humans forget things when doing repetitive work. Using a master copy ensures no important security setting or software gets left out by mistake.

Having a golden snapshot keeps Everyone Safe and Equal. Every employee starts with the exact same trusted, secure setup, making it much easier for IT teams to protect and update all the machines at once.
```

### Step 2 — Same Start, Different Rooms

Your room started identical to everyone else's, and from today it starts to diverge as you work in it.

Explain what stays the same across all the rooms and what becomes yours alone:

```
Every room starts with the exact same walls, doors, lights, and standard furniture. Across all the virtual machines, the underlying operating system, pre-installed tools, basic system settings, and default folders start out 100% identical because they all came from the same master template.

Once I move in and start living there, the room changes based on what you do. The new files you create, programs you install, commands you run, and customization settings you change belong to your room only. Your specific hostname, IP address, and individual user activity make your environment completely unique from everyone else's.
```

---

## Analysis Questions

**Analysis Question 1.** Why does it matter that a standardized image can be *restored*, not just deployed? Describe a realistic situation where restoring from a known-good image is the fastest safe fix. *(Minimum 3 sentences.)*

```
Imagine your computer catches a computer virus, or someone accidentally deletes important files and completely breaks the system. Trying to hunt down every single bug to fix it could take days, and you might still miss something.

Instead of spending hours trying to fix a broken computer, being able to restore a golden image means you can press a giant "reset button." In just a few minutes, it completely wipes away the broken system and replaces it with a brand-new, perfectly working copy so you can get right back to work safely!
```

**Analysis Question 2.** Conceptually, how is a snapshot different from a separate backup? Consider what each one protects against and where each one lives. *(Minimum 3 sentences.)*

```
A snapshot is a point-in-time "photograph" of a system's state that depends on the underlying primary storage, making it ideal for quick rollbacks before making risky software or system changes. In contrast, a separate backup is an independent, complete copy of your data stored on physically or logically isolated secondary storage, protecting against total hardware failures, storage corruption, or site-wide disasters. While a snapshot lives on the same local infrastructure and will fail if the primary drive dies, a backup resides in a separate location so you can fully rebuild your environment even if the original system is completely destroyed.
```

**Analysis Question 3.** Your room was reserved for you rather than created by you. What does that tell you about how cloud access is usually handed out in a real organization, and why would an employer prefer that model? *(Minimum 2 sentences.)*

```
Having a pre-reserved room rather than letting you build your own shows that real organizations use centralized provisioning instead of giving users free-rein admin rights in the cloud.
An employer prefers this approach for three big reasons.

1. Strict Cost & Resource Control: If every employee could create their own cloud servers whenever they wanted, the company would quickly face massive, unexpected cloud bills from abandoned or oversized machines.

2. Enforced Security Baselines: Central IT ensures every pre-allocated environment strictly follows safety policies, eliminating the risk of an employee setting up a misconfigured, vulnerable machine that exposes the whole network.

3. Least-Privilege Management: Assigning users a specific, ready-to-use resource limits their access to only what they need for their job, keeping sensitive administrative controls safely in the hands of the IT team.
```

---

## Submission Checklist

- [x] VM started from My Lab Environment and confirmed **Running** (Part A, Step 1)

- [x] Signed in through Bastion as `analyst` — no credentials recorded anywhere (Part A, Step 2)

- [x] `hostname`, `whoami`, and `pwd` run and outputs recorded (Part A, Steps 3–5)

- [x] Explained what each of the three outputs proves (Part B, Step 1)

- [x] `bastion-session.png` captured, address bar and login data cropped out, uploaded to `assets/screenshots/week-06/` (Part B, Step 2)

- [x] Standardized/golden image explained in your own words (Part C)

- [x] All three Analysis Questions answered (minimum sentence counts met)

- [x] This file is committed to your portfolio repo at `week-06/labs/lab-01-claiming-your-room.md`

---

## GitHub Commit Subsection

1. Open **Week 6 → Lab 01: Claiming Your Room in Cloud Heights** in the Lab Portal.
2. Fill in the worksheet fields — they match this file, in the same order.
3. Connect your GitHub account if you haven't already, and select your portfolio repo.
4. Click **Submit to GitHub**. The Portal commits the completed file to `week-06/labs/lab-01-claiming-your-room.md`.
5. Upload `bastion-session.png` to `assets/screenshots/week-06/` in your repo before you submit.

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
