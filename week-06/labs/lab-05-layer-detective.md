# Week 6 Lab 05 — Layer Detective

**Student Name:** Dan Martinson

**Date Completed:** 8/23/2026

**Module:** 2 — Networking & Cloud Foundations | **Week:** 6  
**Submission Path:** `week-06/labs/lab-05-layer-detective.md`

---

## Overview

**This is a SHORT lab — 20 to 30 minutes — and it needs no VM.** No Cloud Heights session, no simulator, no screenshot. This is a thinking lab: you take the evidence you have already collected in Weeks 5 and 6 and sort it into layers.

This is an **independent** lab.

---

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Environment | This worksheet only — nothing to start, nothing to connect to |
| Prerequisite | Week 5 labs and Week 6 Labs 01–04 |
| Screenshot | None required |

---

## Part A — The Seven-Row Table

Fill in every row. For the last column, name one **real thing you personally saw** in Weeks 5–6 that belongs at that layer.

| # | Layer name | One-line job | Real thing from Weeks 5–6 |
| --- | --- | --- | --- |
| 7 | Application | Provides network services to applications | curl HTTP://10.60.6.4/ |
| 6 | Presentation | Handles data format, encryption, decryption, compression | Data might be encryptedor converted so both sides understand it. |
| 5 | Session | manages the session between systems | starting an ssh session |
| 4 | Transport | End-to-end delivery, reliability, ports | TCP to port 22(ssh), TCP to port 80 (HTTP) |
| 3 | Network | Logical addressing and routing (IP addresses) | My VM (10.60.6.32 wants to reach the Grid Becon (10.60.6.4 or another network.  |
| 2 | Data Link | MAC addressing, frames, switches, ARP | Using ARP to find the MAC address of 10.60.6.4 on the local network |
| 1 | Physical | Cables, Fiber, Wi-Fi signals, electrical/optical signals hardware | Ethernet cable, Wi-Fi radio signals. |

---

## Part B — Case Files

For each case, name the layer where the problem lives, and name the evidence proving the layers **below** it were already working.

### Case File 1 — The Name That Went Nowhere

A hostname lookup fails, but pinging the machine's IP address directly succeeds.

Layer:

```
Layer 7 — Application Layer
```

Evidence that the layers below were working:

```
Evidence Proving Lower Layers Are Working

Layers 1–3 (Physical, Data Link, Network): The successful ICMP ping proves physical cabling/signals (Layer 1) are functional, local MAC address delivery via Ethernet/Wi-Fi (Layer 2) works, and IP routing (Layer 3) successfully delivers packets to and from the destination IP address.
Layer 4 (Transport): ICMP operates alongside Layer 4, showing that basic host-to-host datagram transmission across the network operates without complete packet loss.
```

### Case File 2 — Permission Denied

`ssh` to a host returns `Permission denied` after a password prompt.

Layer:

```
Layer 7 — Application Layer (specifically user authentication, credential checking, or local file access control on the SSH
```

Evidence that the layers below were working:

```
Layers 1–3 (Physical, Data Link, Network): Packets successfully traversed the physical media, local switches, and IP routers to reach the target server and return responses.

Layer 4 (Transport): A full TCP connection (Layer 4) was established on port 22, as shown by the server accepting the socket connection and starting the protocol handshake.
Layers 5 & 6 (Session & Presentation): An active session was initialized and an encrypted cryptographic tunnel (TLS/SSH encryption) was successfully negotiated. This is proven because the server securely transmitted the password prompt to the client, received the user's input, and processed it before rejecting the credentials.
```

### Case File 3 — The Cable Story

A machine reports no link on its interface and has no address at all.

Layer:

```
Layer 1 — Physical Layer (specifically hardware connectivity, such as an unplugged cable, damaged wire/port, disabled NIC, or bad transceiver signal)
```

Evidence and reasoning:

```
None. Because the issue occurs at Layer 1, no underlying layers exist. Since the Physical Layer fails to detect an electrical, optical, or radio signal, higher-level processes—such as MAC address framing (Layer 2) or IP assignment via DHCP (Layer 3)—cannot function at all.
```

### Case File 4 — Ping Works, The Page Does Not

`ping` to a server succeeds, but `curl http://<that server>` returns nothing useful.

Layer:

```
Layer 7 — Application Layer
```

Evidence that the layers below were working:

```
Layers 1–3 (Physical, Data Link, Network): The successful ICMP ping proves physical links (Layer 1), local framing (Layer 2), and IP routing (Layer 3) are functioning properly between the client and server.
Layer 4 (Transport): Running curl attempts a TCP connection on port 80/443. The fact that curl returns a response or fails at the HTTP level—rather than timing out with a "Connection refused" or "No route to host" error—indicates that the underlying TCP handshakes (Layer 4) and sessions (Layer 5) completed successfully.
```

### Case File 5 — Wrong Neighbourhood

A machine has an address, but its default route points somewhere that cannot forward its traffic.

Layer:

```
Layer 3 — Network Layer (specifically routing table configuration/default gateway selection)
```

Evidence and reasoning:

```
Layers 1 & 2 (Physical & Data Link): The device successfully assigned an IP address, meaning its network interface controller (NIC) is functional, physical links (Layer 1) are active, and local frame transmission (Layer 2) works—including ARP requests within its local subnet.
```

---

## Part C — The Silent Gateway Case

In Lab 03 the Azure default gateway did not answer your ping. However, your VM had a valid default route configured, and your local communication with the Grid Beacon — the ping replies, the HTTP banner, and `TRACE ID: CF-NET-0604` — succeeded.

A failed gateway ping is one piece of evidence — not automatically proof of a gateway or network failure. But the evidence you weigh against it has to be the right kind of evidence.

The Grid Beacon at `10.60.6.4` sits on the same local subnet as your VM (`10.60.6.0/26`). Reaching it proves **local-subnet connectivity** — that traffic never crosses the default gateway, so beacon success alone cannot prove the gateway forwarded anything. Your `ip route` output proves a **default route is configured** — your VM knows where it intends to send non-local traffic — but it does not prove the gateway forwarded that traffic. The evidence that demonstrates the **default path is functioning** is successful communication with a destination outside `10.60.6.0/26`, such as the outbound internet access through NAT that you examined in Lab 04.

### Step 1 — Rule on the Case

Is the failed gateway ping enough evidence to declare a network-layer failure? Explain your answer using the other evidence you collected. In your response, distinguish between:

- evidence that proves **local-subnet connectivity**
- evidence that proves a **default route is configured**
- evidence that supports **successful off-subnet connectivity**

```
No, a failed gateway ping is not sufficient evidence to declare a network-layer failure.
In cloud environments like Azure, standard ICMP traffic (ping) to the virtual network's default gateway address is routinely dropped or suppressed by default security policies and host firewalls. A non-responsive gateway IP merely indicates that ICMP echo requests are blocked or ignored by the gateway, not that routing itself is broken.
Evaluating the network status requires distinguishing between the types of collected evidence:
Evidence Proving Local-Subnet Connectivity: Successful ping responses, HTTP banner retrieval, and receiving TRACE ID: CF-NET-0604 from the Grid Beacon (10.60.6.4). Because 10.60.6.4 resides within the local /26 subnet (10.60.6.0/26), layer-2 switches/virtual networks deliver these frames directly. This traffic never reaches or crosses the default gateway, meaning local success cannot confirm gateway routing functions.
Evidence Proving Default Route Configuration: The ip route output. This proves local configuration intent: the virtual machine's OS kernel possesses a valid rule directing non-local destinations to the gateway IP. However, a local routing table entry only proves where the host attempts to send packets—it does not prove the gateway actually receives, processes, or forwards them.
Evidence Supporting Successful Off-Subnet Connectivity: Outbound internet access via NAT (examined in Lab 04). Reaching an external destination outside 10.60.6.0/26 requires the packet to leave the local subnet, hit the default gateway, and be forwarded through the NAT gateway. Successful two-way traffic to a remote IP address serves as concrete proof that the default forwarding path is fully operational despite the silent gateway ping.
```

### Step 2 — Name the Correct Conclusion

For each of these four results, state what it actually proves: the Grid Beacon at `10.60.6.4` answering, the default route shown by `ip route`, a successful connection to a destination outside your local subnet, and the gateway's failed ping. Then state the rule you would give a junior colleague about the difference between an observation ("the gateway did not answer my ICMP probe") and a diagnosis ("the gateway is broken"):

```
Grid Beacon at 10.60.6.4 answering: Proves that Layer 1–3 network connectivity exists to that specific internal host and that its IP stack is active.
Default route shown by ip route: Proves local software configuration only—that the OS kernel knows where to direct non-local traffic. It does not prove the default gateway is reachable or operating properly.
Successful connection to an external destination: Proves end-to-end routing and connectivity outside your local subnet are fully functional, meaning packets are successfully traversing the default gateway regardless of other test anomalies.
Gateway's failed ping: Proves only that ICMP echo requests to the gateway are either blocked (e.g., by a firewall/ACL policy) or ignored. It does not prove the gateway is down, given that external connections are working.

Rule for Junior Colleagues
An observation describes raw telemetry ("what happened"); a diagnosis explains root cause ("why it happened"). Never declare a component broken based on a single failed test when higher-level connectivity succeeds—verify whether the test method itself (such as ICMP) is simply filtered before reaching a conclusion.
```

---

## Part D — Two Models, One Job

The OSI model has seven layers. The practical TCP/IP model most engineers speak day to day has four or five.

### Step 1 — Map Them

Briefly show how the seven OSI layers collapse into the practical model:

```
The 7-layer OSI model collapses into the practical 4-layer (or 5-layer) TCP/IP model by combining upper-layer application functions and lower-layer physical media components:OSI Model (7 Layers)TCP/IP Model (5-Layer)TCP/IP Model (4-Layer Original)Protocols / Examples 7. Application 6. Presentation 5. Session 5. Application 4. ApplicationHTTP, HTTPS, SSH, FTP, DNS, SMTP4. Transport 4. Transport 3. TransportTCP, UDP3. Network 3. Network (Internet) 2. Internet IP (IPv4/IPv6), ICMP, ARP2. Data Link2. Data Link1. Network Access (Link): Ethernet, Wi-Fi (802.11), MAC Addresses 1. Physical 1. Physical
```

### Step 2 — When Each Is Useful

Explain when the seven-layer vocabulary helps and when the practical model is the better tool:

```
The seven-layer OSI model is most useful for systematic network troubleshooting, providing a clear framework to isolate root causes from physical cables up to software. It also serves as a critical teaching tool for abstract concepts and gives vendors a standardized language to classify products, like Layer 4 firewalls versus Layer 7 load balancers. Conversely, the practical TCP/IP model is the better tool for daily engineering because it reflects how modern software actually operates. It avoids artificial separations by merging application, presentation, and session management into a single software-driven layer. Additionally, TCP/IP directly maps to the real-world protocol suite driving the internet, eliminating unnecessary theoretical complexity during actual development.
```

---

## Analysis Questions

**Analysis Question 1.** Explain the Ladder Rule using layer language. What does "test the near thing first" mean when the rungs are layers? *(Minimum 3 sentences.)*

```
The Ladder Rule is a systematic troubleshooting principle applied across layered abstractions—such as software architecture, protocol stacks, or system models—to isolate issues step-by-step rather than jumping randomly through the system. In layer language, each rung of the ladder represents a specific layer of functionality or abstraction, arranged hierarchically from the lowest physical baseline to the highest logical application. Moving up or down the ladder requires verifying that each underlying layer is fully functional before blaming or diagnosing the layer directly above or below it.

In this context, "test the near thing first" means evaluating the immediate adjacent layer—the very next rung down or up from where the issue is observed—rather than skipping across multiple layers to distant assumptions. Because higher-level layers depend strictly on the stability and correct operations of the lower-level layers, isolating an anomaly requires confirming that the nearest foundational layer is working properly. By testing the nearest adjacent layer first, you avoid wasting time diagnosing complex higher-level behaviors when the true root cause is simply a failure in the immediate underlying component
```

**Analysis Question 2.** Why is "which layer is this?" a faster question than "what is broken?" when you are under pressure? *(Minimum 3 sentences.)*

```
Asking "which layer is this?" immediately reduces cognitive load during a crisis by replacing an open-ended hunt with a bounded classification task.
Constrained Problem Space: Asking "what is broken?" invites an infinite number of potential failure scenarios, which leads to analysis paralysis when under high stress. In contrast, "which layer is this?" forces you to categorize the problem into one of a small, fixed set of defined system layers.
Actionable Next Steps: Pinpointing the specific layer immediately dictates the correct diagnostic tools to use 1. using ping for Network layer issues versus inspecting payload formats for Presentation/Application layer issues).
Elimination of Cognitive Bias: It prevents engineers from jumping straight to complex, unverified hypotheses, ensuring the team systematically isolates lower-level dependencies before spending valuable time debugging high-level code.
```

**Analysis Question 3.** Pick one case file from Part B and describe the very next command you would run to confirm your ruling, and what result would change your mind. *(Minimum 2 sentences.)*

```
For Case File 1 (The Name That Went Nowhere), the very next command I would run is nslookup <hostname> (or dig <hostname>) to directly query DNS resolution for the failing hostname. If the command successfully resolves the hostname to its correct IP address, it would change my mind and indicate that DNS itself is working properly, shifting the root cause to a local software issue like a misconfigured hosts file or application-level hostname misconfiguration.
```

---

## Submission Checklist

- [x] All seven rows of the OSI table completed with a real Week 5–6 anchor each (Part A)

- [x] All five case files given a layer and supporting evidence (Part B)

- [x] Silent gateway case ruled on correctly (Part C)

- [x] OSI vs. practical TCP/IP model compared (Part D)

- [x] All three Analysis Questions answered (minimum sentence counts met)

- [x] No screenshot required for this lab

- [x] This file is committed to your portfolio repo at `week-06/labs/lab-05-layer-detective.md`

---

## GitHub Commit Subsection

1. Open **Week 6 → Lab 05: Layer Detective** in the Lab Portal.
2. Fill in the worksheet fields.
3. Click **Submit to GitHub** — the Portal commits to `week-06/labs/lab-05-layer-detective.md`.

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
