# Week 6 Lab 04 — Reading the Blueprints

**Student Name:** Dan Martinson

**Date Completed:** 8/23/2026

**Module:** 2 — Networking & Cloud Foundations | **Week:** 6  
**Submission Path:** `week-06/labs/lab-04-reading-the-blueprints.md`

---

> ### 🔒 Cloud Heights Security Rule
> Your Bastion link and Cloud Heights password are **private access credentials**. Never paste either into a worksheet, screenshot, GitHub repository, Circle post, or chat message. When taking screenshots, crop out the browser address bar and all login information.

---

## Overview

**This is a SHORT lab — 15 to 20 minutes.** It is deliberately small. You already have the commands; this lab is about matching a drawing to reality.

The **Cloud Heights Network Blueprint** is displayed at the top of this lab page in the portal. Everything you write about the network's architecture comes from that blueprint or from your own machine — never from a guess.

---

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Environment | Cloud Heights — live Ubuntu 22.04 VM, reached through Azure Bastion |
| Source of truth | The Cloud Heights Network Blueprint shown at the top of this lab page |
| Commands used | `ip addr`, `ip route` |
| Known value | Student subnet: **`10.60.6.0/26`** |

---

## Part A — Read the Drawing

### Step 1 — Record the Architecture Values

From the blueprint at the top of this page, record each value **exactly as drawn**. If a value is not shown on the blueprint, write "not shown on blueprint" — do not guess.

| Item | Value from the blueprint |
| --- | --- |
| VNet name | vnet-cf-labs |
| VNet address space | Address space: 10.60.6.0/24 |
| Student subnet range | not shown on blueprint |

---

## Part B — Verify Against Your Own Machine

### Step 1 — Confirm Your Address Lives in the Subnet

Run `ip addr` and find your private IPv4 address.

Command and output:

```
analyst@cf-student-07:~$ ip addr
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 60:45:bd:4c:0f:72 brd ff:ff:ff:ff:ff:ff
    inet 10.60.6.26/26 metric 100 brd 10.60.6.63 scope global eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::6245:bdff:fe4c:f72/64 scope link 
       valid_lft forever preferred_lft forever
3: enP7180s1: <BROADCAST,MULTICAST,SLAVE,UP,LOWER_UP> mtu 1500 qdisc mq master eth0 state UP group default qlen 1000
    link/ether 60:45:bd:4c:0f:72 brd ff:ff:ff:ff:ff:ff
    altname enP7180p0s2
```

Your private IP:

```
10.60.6.26
```

Explain how you know your address falls inside `10.60.6.0/26` — what range does that prefix actually cover:

```
My system output shows your IP address is 10.60.6.26 on interface eth0, right alongside a broadcast boundary of 10.60.6.63. Because .26 sits cleanly between the starting network address .0 and the upper limit .63, it sits inside that prefix. It's the same neighborhood.
```

### Step 2 — Confirm Route Behaviour

Run `ip route`.

Command and output:

```
analyst@cf-student-07:~$ ip route
default via 10.60.6.1 dev eth0 proto dhcp src 10.60.6.26 metric 100 
10.60.6.0/26 dev eth0 proto kernel scope link src 10.60.6.26 metric 100 
10.60.6.1 dev eth0 proto dhcp scope link src 10.60.6.26 metric 100 
168.63.129.16 via 10.60.6.1 dev eth0 proto dhcp src 10.60.6.26 metric 100 
169.254.169.254 via 10.60.6.1 dev eth0 proto dhcp src 10.60.6.26 metric 100
```

What the default route tells you about traffic that is not destined for your own subnet:

```
Where to send it Next-Hop the traffic must be sent to gateway address 10.60.6.1, which will handle further routing across other networks.
Which interface to use The packets must exit the system through interface eth0.
What source IP to use the egress packets will use 10.60.6.26 as their originating IP address.
```

### Step 3 — Capture Your Evidence

**Required filename:** `blueprint-verified.png`

This must be **your own `ip addr` and `ip route` output** — not a re-screenshot of the blueprint. Crop out the address bar and any login information.

---

## Part C — How Traffic Actually Moves

### Step 1 — No Public IP

Your VM has a private address and **no public IP**. Explain what that means for who can reach it directly from the internet:

```
Because my VM only has a private IP address, no external devices on the public internet can initiate a direct connection to it or reach it using standard internet routing. Devices on the internet cannot address my virtual machine directly since private IP ranges like 10.60.6.0/26 are non-routable across the global web and exist strictly inside my internal Virtual Network (VNet). Anyone needing to reach the VM from the outside must go through a secure intermediate gateway, such as Azure Bastion.
```

### Step 2 — Outbound vs. Inbound

Outbound internet traffic from your VM leaves through address **translation (NAT)**. Inbound access for you arrives through **Azure Bastion**, not through a public address on the VM.

Explain both directions in your own words:

```
When outbound traffic leaves the VM, network address translation (NAT) takes the machine's private internal IP address (10.60.6.26) and translates it into a shared, public IP address so it can reach external resources on the internet. Return traffic from those outbound requests is mapped back to the VM, but external devices on the internet cannot use that public NAT address to initiate a new, unsolicited connection back to the VM. For inbound access, administrative connections do not hit the VM directly over a public IP; instead, users connect securely to Azure Bastion over HTTPS through a browser, and Bastion proxies that SSH management session directly to the VM's private IP inside the internal network.
```

### Step 3 — The Guard Post You Do Not Touch Yet

Each student machine sits behind its own **network security group** — a per-student guard post that decides what traffic is allowed in.

**In Week 6 you do not configure it.** Week 7 is when you take control of those rules.

Write one sentence naming what the guard post does and one sentence stating what you are *not* doing with it this week:

```
The Network Security Group (NSG) acts as a virtual firewall that evaluates inbound network traffic against specific security rules to permit or block access to the virtual machine. During Week 6, I am not modifying, adding, or managing any of the configuration rules on this guard post.
```

---

## Analysis Questions

**Analysis Question 1.** Why would an organization put every student machine in one small subnet instead of giving each machine a public address? *(Minimum 3 sentences.)*

```
Placing every student machine in a single, small private subnet rather than assigning individual public IP addresses provides crucial security, operational, and financial advantages. Using private IPv4 addresses shields the VMs from the public internet, preventing external attackers from discovering or directly initiating unauthorized connections to the student environments. Public IPv4 addresses are scarce and incur additional costs from cloud providers like Azure, so sharing a small private subnet alongside NAT translation minimizes infrastructure expenses and optimizes address allocation. Grouping student VMs within a unified subnet simplifies network management and administrative oversight, allowing instructors to enforce consistent security rules, monitor internal traffic, and manage access through centralized gateways like Azure Bastion.
```

**Analysis Question 2.** Segmentation means separating a network into parts that cannot freely reach each other. Give one concrete benefit of segmentation during a security incident. *(Minimum 3 sentences.)*

```
During a security incident, one concrete benefit of network segmentation is limiting lateral movement to contain the breach within a localized zone. If an attacker or malware compromises a single host in a segmented network, strict access controls and firewalls prevent them from freely scanning or pivoting into other subnets containing critical systems or sensitive data. This isolation grants the incident response team valuable time to detect, investigate, and remediate the threat before the compromise can escalate across the entire infrastructure.
```

**Analysis Question 3.** A diagram and a live machine disagree about an address range. Which do you trust, what do you do next, and why? *(Minimum 2 sentences.)*

```
I trust the live machine because active network traffic and routing decisions operate based on real-time system state rather than static planning documents.
I would verify the configuration directly on the host using network commands such as ip addr and ip route, and investigate why the documentation is outdated.

You do this because diagrams can easily become legacy artifacts during unrecorded network updates, whereas the running kernel dictates how traffic actually moves through the network.
```

---

## Submission Checklist

- [x] VNet name, address space, and subnet range recorded from the blueprint (Part A)

- [x] `ip addr` run and own private IP confirmed inside `10.60.6.0/26` (Part B, Step 1)

- [x] `ip route` run and default route behaviour explained (Part B, Step 2)

- [x] `blueprint-verified.png` captured from your own terminal, cropped, uploaded to `assets/screenshots/week-06/` (Part B, Step 3)

- [x] Private address / NAT / Bastion explained (Part C, Steps 1–2)

- [x] Per-student guard post identified — and explicitly not configured this week (Part C, Step 3)

- [x] All three Analysis Questions answered (minimum sentence counts met)

- [x] This file is committed to your portfolio repo at `week-06/labs/lab-04-reading-the-blueprints.md`

---

## GitHub Commit Subsection

1. Open **Week 6 → Lab 04: Reading the Blueprints** in the Lab Portal.
2. Fill in the worksheet fields and upload `blueprint-verified.png` to `assets/screenshots/week-06/`.
3. Click **Submit to GitHub** — the Portal commits to `week-06/labs/lab-04-reading-the-blueprints.md`.

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
