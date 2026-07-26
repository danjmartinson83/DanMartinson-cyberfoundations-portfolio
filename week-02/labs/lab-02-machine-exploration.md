# Week 2 Lab 02 — Explore Your Own Machine (Real Specs & Live Activity)

**Student Name:** Dan Martinson

**Date Completed:** 7/26/2026

**Module:** 1 — Digital Infrastructure & CLI | **Week:** 2  
**Submission Path:** `week-02/labs/lab-02-machine-exploration.md`

---

## Overview

Lab 01 got you diagramming how hardware, OS, and software interact — in theory. This lab makes it real, in one sitting. First, you'll look up your own machine's actual specs (OS version, RAM, storage) using its built-in settings screens. Then you'll open Task Manager (Windows) or Activity Monitor (Mac) and watch those same hardware and software layers working together live — CPU usage, memory usage, and real running processes — and connect what you see back to your Lab 01 diagram.

**No terminal or command line is required this week** — that starts in Week 3. Settings screens, Task Manager, and Activity Monitor are all point-and-click tools.

---

## Lab Environment

| Component | Details |
|---|---|
| Environment | Your own computer (Windows or Mac) — no VM, no cloud, no install needed |
| Required Materials | Your computer's built-in Settings/About screen; Task Manager (Windows: `Ctrl+Shift+Esc`) or Activity Monitor (Mac: `Cmd+Space`, then type "Activity Monitor") |

**Prerequisite:** Lab 01 completed — you'll reference your diagram in this lab's Analysis Questions. Fill out this worksheet here in the Lab Portal, then hit Submit to commit it directly to your repo at `week-02/labs/lab-02-machine-exploration.md`.

---

## Part A — Find Your Real Specs

**Before you start:** here's what to expect so you don't second-guess yourself. On Windows, you're looking for a page titled **About**, reached via **Settings → System → About**, listing your device specs under "Device specifications." On Mac, you're looking for a window titled **About This Mac** (click the Apple menu, top-left corner), with an Overview tab listing your chip, memory, and macOS version. If what's on your screen doesn't roughly match that, you're in the wrong menu — try again before recording anything below.

### Step 1 — Find Your OS Version

Open your computer's system settings (Windows: **Settings → System → About**. Mac: **Apple menu → About This Mac**) and find the exact operating system name and version you're running.

**OS and version:** Answers are listed below.

```
Microsoft Windows 11 Home
Version 10.0.26200 Build 26200
```

### Step 2 — Check Your Installed RAM

On the same settings screen, find how much RAM (memory) is installed on your computer.

**Installed RAM:** 12GB Installed Physical Memory RAM

```
My device has 12GB / 11.8GB available installed physical memory RAM
```

### Step 3 — Check Your Available Storage

Find your computer's total storage capacity and how much is currently free (Windows: **Settings → System → Storage**. Mac: **About This Mac → Storage**).

**Total storage:** 386 GB of 477 GB used

```
386 GB of 477 GB used 
```

**Free storage:** 87.9 GB free

```
87.9 GB free
```

---

## Part B — Watch It Live

Your Part A numbers are a snapshot. This part shows those same layers actually working, moment to moment.

### Step 1 — Open Task Manager or Activity Monitor

Windows: press `Ctrl+Shift+Esc`. Mac: press `Cmd+Space`, type "Activity Monitor," and press Enter.

### Step 2 — Find the Performance / CPU Tab

Windows: click the **Performance** tab. Mac: click the **CPU** tab.

### Step 3 — Freeze the List Before You Read It

The process list updates constantly and can be hard to read while it's jumping around. Before recording anything, click the **Name** column header (or **Memory**, if you'd rather sort by what's using the most RAM) to sort the list — this won't stop it from updating, but it keeps things from reordering under you while you read.

### Step 4 — Record CPU Usage

Look at the current CPU usage percentage.

**Current CPU usage:** 15% 2.42GHz

### Step 5 — Record Memory Usage

Find how much RAM is currently in use, out of your total installed RAM (the same total you looked up in Part A).

**RAM currently in use:** 9.4GB

**Total installed RAM (from Part A):** 12GB of RAM installed

### Step 6 — List Five Running Processes

List five processes running right now. For each, write your best guess at what it is or does — you don't need to be 100% correct, just reason it out. If you spot something on the cheat sheet below, you can use that, but try at least a couple you don't recognize.

*Cheat sheet — common processes you'll likely see (not exhaustive, just a starting reference):*

| Process Name | Usually Seen On | What It Generally Is |
|---|---|---|
| explorer.exe | Windows | The Windows desktop and file browser itself — normal, always running |
| svchost.exe | Windows | A generic host for background Windows services — several running at once is normal |
| Antimalware Service Executable | Windows | Windows Defender scanning files in the background — normal |
| dwm.exe | Windows | Desktop Window Manager — handles visual effects like transparency and window animations |
| System Idle Process | Windows | Not a real program — represents how much CPU is doing *nothing* right now |
| WindowServer | Mac | Manages everything drawn on your screen — always running |
| Finder | Mac | The Mac desktop and file browser itself — normal, always running |
| mdworker / mds | Mac | Spotlight's background indexing service — normal, can spike briefly after installing apps |
| launchd | Mac | The very first process Mac starts — manages and launches other background services |

*Your five processes:*

| # | Process Name | What I Think It Does |
| --- | --- | --- |
| 1 | zoom  | It is a program that allows meetings to happen between several devices. |
| 2 | McAfee VPN | Encrypts internet traffic, hides your IP Address, secures unsafe networks |
| 3 | Grammarly | It helps check for spelling or grammar mistakes |
| 4 | Windows explorer | Helps organize and hold diffrent folders and files that can be explored by me |
| 5 | Task manager | It tracks how hard your computer's components are working in real-time, manages running programs and processes, and It allows you to view and manage which programs automatically launch when you turn on your computer, helping you disable unnecessary apps to speed up boot times. |

### Step 7 — Screenshot and Embed

This step happens directly on GitHub, not through this worksheet — there's no upload field here, since screenshots are added through GitHub's own upload UI.

1. Go to your portfolio repository on GitHub.com and navigate to `assets/screenshots/week-02/`.
2. Click **Add file → Upload files**, then drag in your screenshot (name it something descriptive, like `machine-exploration.png`).
3. Commit the upload.
4. Click on the uploaded image to open it, then click the **Raw** button. Copy the URL from your browser's address bar.
5. After you submit this worksheet, it will be committed to your repo. Go back to GitHub, open the committed file, click the pencil (edit) icon, and paste your raw URL into the embed line below:

```markdown
![Task Manager / Activity Monitor screenshot](paste your raw image URL here)
```

**My Screenshot** (added directly on GitHub after you submit):

### Step 8 — Connect the Numbers

In your own words, explain how the real numbers you found in Part A (OS version, RAM, storage) relate to what you just watched live in Part B. Which number describes hardware, and which describes the OS?

```
From the numbers listed above, I see I need to clean up some of my unused apps in permanent storage.  I also need to clear out my temp files for better overall performance.
```

---

## Analysis Questions

### Analysis Question 1

Pick one process from your list in Part B, Step 6. Is it "software" in the sense Lab 01 used that word? Explain how it depends on the OS and on hardware to actually run.

```
Windows Explorer depends on the OS to communicate with the RAM and to make changes in files. I am changing or adding files into permanent storage. This includes the snipping tool I used to take screenshots of my screen to complete this lab.
```

### Analysis Question 2

Your CPU usage number changes constantly, even when you're not doing anything. Explain, in your own words, why watching this number matters for security work — not just for performance. (Hint: think about what it might mean if a process you don't recognize suddenly spikes CPU usage.)

```
CPU usage numbers show how active the computer is and with which files. Some processes take more CPU usage than others.  This is important in security work because if you see a spike and you are doing nothing on your computer, it could mean malware or other issues or processes such as unauthorized commands are taking place on your own computer that I would not even be aware of. Also, what it does and what it is accessing and making your computer do.
```

### Analysis Question 3

Compare what you saw in Task Manager/Activity Monitor to the diagram you built in Lab 01. What's the same? What did watching your machine live show you that a static diagram couldn't?

```
The task manager and activity monitor both show overall usage.  The task manager shows what processes are taking the most memory by process. It also shows me the different layers working together to operate my computer. Right now Google Chrome is using the most memory.
```

---

## Submission Checklist

- [x] OS version, installed RAM, and total/free storage looked up and recorded (Part A)

- [x] Task Manager or Activity Monitor opened and list sorted before recording (Part B)

- [x] Current CPU usage recorded

- [x] Current RAM usage recorded, alongside total RAM from Part A

- [x] Five running processes listed, each with a reasoned guess at what it does

- [x] Screenshot uploaded to `assets/screenshots/week-02/` via GitHub and embedded directly in the committed file

- [x] Connection explanation written (Part B, Step 8 — minimum 2 sentences)

- [x] All three Analysis Questions answered (minimum sentence counts met)

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
