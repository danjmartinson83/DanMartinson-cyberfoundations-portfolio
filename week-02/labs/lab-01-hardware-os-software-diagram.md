# Week 2 Lab 01 — Cybersecurity Landscape & Digital Infrastructure Overview

**Student Name:** Dan Martinson

**Date Completed:** 7/23/2026

**Module:** 1 — Digital Infrastructure & CLI | **Week:** 2  
**Submission Path:** `week-02/labs/lab-01-hardware-os-software-diagram.md`

---

## Overview

In this lab, you build a working mental model of the system you'll be securing throughout this course: the hardware, operating system, and software layers that make up every computer, and where the cybersecurity field fits around them. This lab has two parts. Part A connects this week's material to the CyberFoundations City map. Part B has you build and explain a diagram of how a computer's hardware, OS, and software layers interact.

**No terminal or command line is required this week** — that starts in Week 3.

---

## Lab Environment

| Component | Details |
|---|---|
| Environment | Browser-based Lab Portal (Module 1 orientation) |
| Required Materials | CyberFoundations City map; a diagram tool of your choice (hand-drawn and photographed, or any digital tool) |

**Prerequisite:** Portfolio repo created from the CyberFoundations student template in Week 1. Fill out this worksheet here in the Lab Portal, then hit Submit to commit it directly to your repo at `week-02/labs/lab-01-hardware-os-software-diagram.md`.

---

## Part A — CyberFoundations City & the Cybersecurity Landscape

The CyberFoundations City map is your visual guide to the next 11 weeks. Each district represents a module of this course. This part connects this week's material to the map you were introduced to in Week 1.

### Step 1 — Open the Lab Portal Orientation Module

From your Student Dashboard, open the **Module 1 orientation** module.

### Step 2 — Complete the Orientation Walkthrough

Work through the orientation content. It covers the same hardware/OS/software material as this week's lessons from a different angle — use it to check your understanding, not to replace the lessons.

### Step 3 — Locate This Week's District on the City Map

Open the CyberFoundations City map (introduced in Week 1, Lesson 6). Identify which district corresponds to Module 1 — Digital Infrastructure & CLI.

**District name:** Foundry District

```
Foundry District is this weeks district we are learning in.
```

**Why this district fits this week's topics (1–2 sentences):** I am learning the fundamental parts of both hardware what they are and what they do.  I am also learning about different operating systems.

```
The motherboard acts as the hardware that is the main circuit board connecting every component together. Acting as fundamental infrastructure for key components such as the CPU, RAM, and storage.  
```

---

## Part B — Hardware, OS, and Software Diagram

A computer is a stack of layers: physical hardware at the bottom, an operating system managing that hardware in the middle, and the software you actually use on top. This part has you draw that stack and explain it in your own words.

### Step 1 — Identify the Layers

Before drawing anything, name one example of what lives at each layer.

**Hardware layer — one example component (e.g., CPU, RAM, or storage):** RAM

```
Short-term high-speed memory for whatever a program is actively working on right now. RAM is cleared completely when power is off.
```

**Operating system layer — name an OS (e.g., Windows, Linux, or macOS):** Windows

```
Windows is a common desktop OS used in offices and on personal computers.  Its Graphical interface supports point-and-click use.  
```

**Software layer — one example application (e.g., a web browser or word processor):** Word Processor

```
A word processor like Microsoft Word is a program that uses its program to help develop word documents.  While typing and editing text documents for all personal and professional needs. It is a program that is the top layer of the layers.  It also uses the OS layer while using it and the hardware layer as your work is saved into the storage.   
```

### Step 2 — Sketch Your Diagram

Sketch a simple diagram (hand-drawn and photographed, or built in any digital tool) showing how the hardware, OS, and software layers stack and interact. Arrows or labels showing "what talks to what" matter more than visual polish. If you'd like a free browser-based option instead of hand-drawing, try [draw.io](https://www.drawio.com/) — no account required to get started.

### Step 3 — Upload and Embed Your Diagram

This step happens directly on GitHub, not through this worksheet — there's no upload field here, since screenshots and diagrams are added through GitHub's own upload UI, the same way as every other week.

1. Go to your portfolio repository on GitHub.com and navigate to `assets/screenshots/week-02/`.
2. Click **Add file → Upload files**, then drag in your diagram image (name it something descriptive, like `hardware-os-software-diagram.png` — no spaces, lowercase, no timestamps).
3. Commit the upload.
4. Click on the uploaded image to open it, then click the **Raw** button. Copy the URL from your browser's address bar.
5. After you submit this worksheet, it will be committed to your repo. Go back to GitHub, open the committed file, click the pencil (edit) icon, and paste your raw URL into the embed line below:

```markdown
![Hardware/OS/software diagram](paste your raw image URL here)
```

**My Diagram** (added directly on GitHub after you submit):

### Step 4 — Explain Your Diagram

In your own words — not a copied definition — explain how the three layers interact. Reference your own diagram directly.

**Explanation (minimum 3 sentences):** Layers and how they work.

```
With the hardware plugged into the motherboard correctly and with power.
The hardware layer contains the CPU, RAM, and storage memory.  Through Kernel communications and device drivers, the hardware layer passes data and interrupts data. 
The OS layer Windows, macOS, or Linux manages Hardware controls.  The OS layer receives requests and services and provides services to the software after passing through the hardware. The OS also runs the software layer, handling communications from the hardware and software, helping keep things organized and running.
The software level is where the user uses the Programs installed and the services it offers, operated by the OS.       
```

---

## Analysis Questions

Answer each question in your own words. These questions connect what you did in Parts A and B to the bigger picture of this course.

### Analysis Question 1

If the operating system crashed on the computer you diagrammed, which layer(s) would stop working, and which (if any) would keep working? Explain your reasoning.

```
If the operating system crashed on the computer the software would not work on the computer because it is dependent on the OS layer of the computer to operate. The OS layer would stop doing its job of handling the software and its communications with the hardware.  All work and RAM memory would not be saved but the information in the Storage memory would still be intact.  
```

### Analysis Question 2

Pick one piece of software you use daily. Trace it down through the OS to the hardware it ultimately depends on. What would happen to that software if the hardware layer failed?

```
I use Microsoft Word for my software. Word is dependent on the Windows OS, and it cannot work correctly with a hardware failure due to a lack of communication with the CPU, RAM, or Storage.  This would cause a system crash, making all unsaved work lost, and depending on what failed in the hardware layer, your work overall. (Storage disk failure)   
```

### Analysis Question 3

Explain, in your own words, why a cybersecurity professional needs to understand all three layers — hardware, OS, and software — rather than just the software layer where most visible attacks (like phishing emails) happen.

```
Cybersecurity professionals need to understand all three layers because some attacks not only hit the software level.  Some can change or install programs in the background that can lock up the OS and make changes to usernames and passwords, locking the user out.  Some security failures can allow the hardware to become overwhelmed or destroy the CPU, RAM, or long-term memory.  Knowing which layer is being attacked, where it started, and what the threat did is how cybersecurity professionals can protect the system in the future.  
```

---

## Lab Report Questions

Answer each question in complete sentences.

**1. What is the cybersecurity landscape, and why does it matter to someone starting this course?**

```
The cybersecurity landscape refers to the (Big Picture) entire ecosystem of digital environments, threats, vulnerabilities, defense mechanisms, and regulations that exist today. It encompasses everything from individual devices and local networks. Remember Hospitals, Schools, Public services, and Banks use these systems as well as users at work and home. Attackers, defenders, infrastructure, and everyday users are some of the people who use or try to use the landscape every day.  Understanding this landscape matters at the start of this course because it provides the big-picture context for why specific technical skills are necessary. This knowledge can help a person in this course understand how to prevent threats, detect suspicious activity, respond, recover, and improve the landscape.
```

**2. Which CyberFoundations City district did you identify in Part A, and how does its theme connect to the hardware/OS/software material in Part B?**

```
The Foundry District understanding is of the computer and the different layers of a computer, and which layer does what. Understanding the attack surface and how vulnerable each layer is in the landscape, as well as each layer of the computer also. This connects because from the phones, laptops, desktops, data centers, even clouds we use every day are all connected to these three layers in part B.  I like to think of the castle vs CyberFoundations city and the number of entryways into it.
```

**3. Of the three layers (hardware, OS, software), which one do you think is hardest to secure, and why?**

```
I think the software layer is the hardest to secure.  Attackers use the largest attack surface that is constantly changing. If your using e-mail that is part of the software layer, you could easily click on something that gives unauthorized access to many different things in so many ways. Usernames, passwords, account information, sensitive files, information, and data.  
```

---

## Submission Checklist

- [x] Lab Portal Module 1 orientation completed

- [x] District identified and explained

- [x] Hardware, OS, and software layer examples listed

- [x] Diagram uploaded to `assets/screenshots/week-02/` via GitHub and embedded directly in the committed file

- [x] Diagram explanation written in your own words (minimum 3 sentences)

- [x] All three Analysis Questions answered (minimum sentence counts met)

- [x] All three Lab Report Questions answered in complete sentences

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
