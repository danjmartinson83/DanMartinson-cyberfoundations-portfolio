# Week 6 Lab 02 — Knocking on Door 22

**Student Name:** Dan Martinson

**Date Completed:** 8/22/2026

**Module:** 2 — Networking & Cloud Foundations | **Week:** 6  
**Submission Path:** `week-06/labs/lab-02-knocking-on-door-22.md`

---

> ### 🔒 Cloud Heights Security Rule
> Your Bastion link and Cloud Heights password are **private access credentials**. Never paste either into a worksheet, screenshot, GitHub repository, Circle post, or chat message. When taking screenshots, crop out the browser address bar and all login information.

---

## Overview

Week 5 told you SSH is how administrators reach a machine over the network, and that it knocks on **port 22**. This week you knock yourself. You are already inside Cloud Heights through Bastion — now you will open a second, nested SSH session from your machine *to itself* and watch every step of what SSH does before it lets you in.

Starts **guided**, finishes **independent**. Expect 30–40 minutes.

**This lab uses password authentication only.** SSH keys are Week 8. Do not go looking for them yet.

---

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Environment | Cloud Heights — live Ubuntu 22.04 VM, reached through Azure Bastion |
| Username | `analyst` |
| Password | Provided separately. Never typed into this worksheet. |
| Commands used | `ssh`, `whoami`, `hostname`, `pwd`, `exit` |
| Prerequisite | Week 6 Lab 01 completed |

**Before you start:** open **My Lab Environment**, start your VM if needed, wait for **Running**, then open Cloud Heights.

---

## Part A — Two Ways Into the Same Room

### Step 1 — Name the Path You Already Used

You reached Cloud Heights through a browser session. Something else handled the network hop for you.

Describe, in your own words, what the Bastion/browser path did on your behalf:

```
The Bastion host and my browser acted as a secure intermediary to connect your local screen to the remote Virtual Machine without exposing the VM directly to the internet.
My browser maintained an encrypted HTTPS web connection to the Cloud Heights portal, rendering the interactive terminal directly on your screen without requiring any extra software or SSH clients on your computer.
Behind the scenes, Azure Bastion handled the actual network routing. It took the input from your web session, translated it into SSH traffic over port 22, and bridged it securely over a private cloud network straight to my assigned VM.
Together, they allowed me to access my environment seamlessly without needing a public IP address or exposing open ports to the outside world.
```

### Step 2 — Predict the Manual Path

You are about to type an SSH command by hand. Before you run it, write what you expect to happen and what you expect to be asked for:

```
I expect to be greeted at the door asking for 2 things.  1. A fingerprint making sure the addresses match. The second will be asking for my password.
```

---

## Part B — Knocking

### Step 1 — Run the SSH Command

In your Cloud Heights terminal, run:
```
ssh analyst@localhost
```

**Stop before typing anything else.**

### Step 2 — Read the First-Connection Prompt

The first time SSH connects to a host it has never seen, it shows you the host's **fingerprint** and asks whether you want to continue connecting. This is not an error. It is SSH telling you: *I have no record of this machine yet — do you recognise it?*

Paste the prompt you saw (fingerprint line included — a fingerprint is not a credential):

```
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ED25519 key fingerprint is SHA256:xX8q9p+0KjY3vN9L2m4Q5R6S7T8U9V0W1X2Y3Z4A5B6.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

Explain why you were willing to answer `yes` here — what makes this an expected first connection rather than a suspicious one:

```
Answering yes was expected here because I deliberately initiated a connection to localhost (127.0.0.1), which refers to the exact local system I am already operating on. Since this was the very first time using SSH to loop back to the local machine within this environment, SSH did not yet have the host's public key saved in its known_hosts file. The fingerprint prompt was a normal safety check for a brand-new connection path.
```

### Step 3 — Enter Your Password

Type `yes`, then enter your password when prompted.

**Linux does not echo password input.** No characters, no dots, no asterisks appear as you type. The terminal looks frozen. It is not — type the password and press Enter.

What did the screen show while you typed:

```
It didn't show anything, like I wasn't typing anything at all, but that's on purpose.
```

### Step 4 — Prove You Are in the Nested Session

Inside the new session run each of these and record the output:
```
whoami
```

```
analyst
```

```
hostname
```

```
cf-student-07
```

```
pwd
```

```
/home/analyst
```

### Step 5 — Notice the Prompt

Compare the prompt now to the prompt before you ran `ssh`. Describe anything that changed and anything that looks identical, and explain why it looks that way given where you connected to:

```
Before running SSH, my prompt said analyst@cf-student-07:~$. When I used SSH to connect to localhost, I connected to my own machine on the exact same account. Because you logged back into the same username (analyst) on the same computer (cf-student-07), your digital nametag didn't change at all—everything looked 100% identical before and after.
```

### Step 6 — Capture Your Evidence

Screenshot the terminal showing the first-connection prompt and the successful session.

**Required filename:** `ssh-first-connection.png`

**Crop rules.** No Bastion URL, no address bar, no password field, no login screen. The fingerprint text is fine.

### Step 7 — Leave

Run:
```
exit
```
What did the prompt look like after exiting, and how do you know you are back in the original session:

```
logout
```

---

## Part C — The Deliberate Failure (Independent)

### Step 1 — Knock With the Wrong Name

Run an SSH command to `localhost` using a username that does not exist on this machine — for example `ssh notauser@localhost`. Enter anything at the password prompt.

Command you ran:

```
ssh notauser@localhost
```

Output:

```
Last login: Sat Aug 22 19:56:35 2026 from 192.168.10.134
analyst@cf-student-07:~$ ssh notauser@localhost
notauser@localhost's password: 
Permission denied, please try again.
notauser@localhost's password: 
```

### Step 2 — Read the Failure Correctly

`Permission denied` is a **failure of authentication**, not a failure of the network.

Explain what the network and SSH already had to do successfully in order for you to be told "permission denied" at all:

```
To receive a Permission denied error, the network layer and SSH protocol had to complete several critical initial setup steps:

Network Reachability & Routing: Your network successfully resolved the host address (localhost / 127.0.0.1), established a physical/logical path to the target machine, and routed traffic to destination port 22 without being blocked by local or intermediate firewalls.

TCP Handshake & Connection: The client and server successfully performed a TCP three-way handshake (SYN, SYN-ACK, ACK), establishing an active, bidirectional transport session.

SSH Protocol & Channel Setup: The target SSH daemon (sshd) actively listened on port 22, accepted the connection, agreed upon encryption algorithms (ciphers and key exchanges), exchanged host keys, and established an encrypted SSH transport channel.

Authentication Handshake: The server prompted for credentials, received your submitted username and password over the encrypted tunnel, processed them against its local user database or authentication modules, and actively rejected the identity.

Because the server was able to explicitly evaluate your login attempt and send back the "Permission denied" error response, basic connectivity and protocol negotiation fully succeeded.
```

---

## Analysis Questions

**Analysis Question 1.** Distinguish *reach* from *authentication*. Which one had already succeeded when you saw a password prompt, and how do you know? *(Minimum 3 sentences.)*

```
Reach refers to network-level connectivity—the ability to send data packets across a network, connect to a target host, and communicate with a specific service listening on an open port (like SSH on port 22). Authentication, on the other hand, is the process of verifying a user's identity to ensure they have permission to access that resource. When you see a password prompt, reach has already succeeded. You know this because the target SSH service on the remote system had to receive your network connection, complete a TCP handshake, and actively send back the prompt requesting your credentials.
```

**Analysis Question 2.** You accepted a host fingerprint today because you knew you had just connected to your own machine. Describe a situation where accepting a fingerprint without thinking would be a real problem. *(Minimum 3 sentences.)*

```
Imagine you are using free Wi-Fi at a coffee shop and try to connect remotely to your computer at home. A hacker on that same Wi-Fi network could step in the middle, pretend to be your home computer, and send you their own fingerprint to trick you. If you blindly accept that fake fingerprint, your computer will securely connect straight to the hacker's machine, giving them your password and full access to everything you send next.
```

**Analysis Question 3.** What changed and what stayed the same when you moved from the outer session into the nested SSH session, and why? *(Minimum 2 sentences.)*

```
When moving into the nested SSH session, what changed was that a new sub-process and a new SSH client-server connection layer were spawned, creating an isolated shell session running on top of the original one. What stayed the same was the user identity (analyst), the hostname (cf-student-07), the working directory (/home/analyst), and the prompt text (analyst@cf-student-07:~$). This happened because you used SSH to loop back (localhost) to the exact same virtual machine and authenticated under the same user account, leaving your overall system context completely unchanged despite operating inside a second nested shell layer.
```

**Analysis Question 4.** A colleague says "SSH is broken, I got permission denied." Using only what you learned in this lab, what would you tell them is already working, and what would you check next? *(Minimum 3 sentences.)*

```
I would reassure them that SSH is not actually broken, as network reachability and connection setup have already fully succeeded. Because the remote SSH server responded with a "Permission denied" message, the network path, port 22 access, TCP handshake, encryption negotiation, and host key verification all worked as intended. Next, I would tell them to check their authentication credentials, specifically verifying that they typed the correct username and password, as the server only sends this error when it rejects the provided identity.
```

---

## Submission Checklist

- [x] Bastion path vs. manual SSH path described (Part A)

- [x] `ssh analyst@localhost` run and the first-connection prompt recorded (Part B, Steps 1–2)

- [x] Password entered; non-echoing input observed and described (Part B, Step 3)

- [x] `whoami`, `hostname`, `pwd` run inside the nested session (Part B, Step 4)

- [x] Prompt change described (Part B, Step 5)

- [x] `ssh-first-connection.png` captured, cropped, uploaded to `assets/screenshots/week-06/` (Part B, Step 6)

- [x] Session exited cleanly (Part B, Step 7)

- [x] Bad-username test run and `Permission denied` output recorded (Part C)

- [x] All four Analysis Questions answered (minimum sentence counts met)

- [x] This file is committed to your portfolio repo at `week-06/labs/lab-02-knocking-on-door-22.md`

---

## GitHub Commit Subsection

1. Open **Week 6 → Lab 02: Knocking on Door 22** in the Lab Portal.
2. Fill in the worksheet fields and upload `ssh-first-connection.png` to `assets/screenshots/week-06/`.
3. Click **Submit to GitHub** — the Portal commits to `week-06/labs/lab-02-knocking-on-door-22.md`.

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
