# Week 6 Lab 03 — The Grid, For Real

**Student Name:** Dan Martinson

**Date Completed:** 8/22/2026

**Module:** 2 — Networking & Cloud Foundations | **Week:** 6  
**Submission Path:** `week-06/labs/lab-03-the-grid-for-real.md`

---

> ### 🔒 Cloud Heights Security Rule
> Your Bastion link and Cloud Heights password are **private access credentials**. Never paste either into a worksheet, screenshot, GitHub repository, Circle post, or chat message. When taking screenshots, crop out the browser address bar and all login information.

---

## Overview

In Week 5 you ran `ip addr`, `ip route`, `ping`, and `traceroute` in a simulator that always behaved. Today you run the same toolkit against real cloud infrastructure that does **not** always behave the way the textbook implies — and you learn to tell "broken" apart from "normal."

This is an **independent** lab. It tells you what to accomplish; you choose the commands. Expect about 40 minutes.

---

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Environment | Cloud Heights — live Ubuntu 22.04 VM, reached through Azure Bastion |
| Commands used | `ip addr`, `ip route`, `ping`, `traceroute`, `curl` |
| Known-good target | **Grid Beacon — `10.60.6.4`** |
| Prerequisite | Week 6 Labs 01–02 |

---

## Part A — Where You Actually Are

### Step 1 — Read Your Own Address

Run the command that lists your interfaces and addresses.

Command and output:

```
ip addr
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
3: enP7232s1: <BROADCAST,MULTICAST,SLAVE,UP,LOWER_UP> mtu 1500 qdisc mq master eth0 state UP group default qlen 1000
    link/ether 60:45:bd:4c:0f:72 brd ff:ff:ff:ff:ff:ff
    altname enP7232p0s2
ip route
analyst@cf-student-07:~$ ip route
default via 10.60.6.1 dev eth0 proto dhcp src 10.60.6.26 metric 100 
10.60.6.0/26 dev eth0 proto kernel scope link src 10.60.6.26 metric 100 
10.60.6.1 dev eth0 proto dhcp scope link src 10.60.6.26 metric 100 
168.63.129.16 via 10.60.6.1 dev eth0 proto dhcp src 10.60.6.26 metric 100 
169.254.169.254 via 10.60.6.1 dev eth0 proto dhcp src 10.60.6.26 metric 100 
pwd
analyst@cf-student-07:~$ pwd
/home/analyst

```

Your private IPv4 address and prefix length:

```
10.60.6.26/26
```

### Step 2 — Read Your Route

Run the command that shows the routing table.

Command and output:

```
analyst@cf-student-07:~$ ip route
default via 10.60.6.1 dev eth0 proto dhcp src 10.60.6.26 metric 100 
10.60.6.0/26 dev eth0 proto kernel scope link src 10.60.6.26 metric 100 
10.60.6.1 dev eth0 proto dhcp scope link src 10.60.6.26 metric 100 
168.63.129.16 via 10.60.6.1 dev eth0 proto dhcp src 10.60.6.26 metric 100 
169.254.169.254 via 10.60.6.1 dev eth0 proto dhcp src 10.60.6.26 metric 100 
```

Your default gateway:

```
default via 10.60.6.1 dev eth0 
```

### Step 3 — Compare to Week 5

Compare this live Ubuntu output to what the CLI Simulator produced in Week 5. What looks the same, what looks different, and what surprised you:

```
What looks the same.
Both the live Ubuntu output and the CLI Simulator show the primary default route pointing to a default gateway via eth0 (default via 10.60.6.1 dev eth0), as well as the local subnet entry (10.60.6.0/26). The core routing logic—directing out-of-network traffic through the default gateway interface—remains identical in structure to what was simulated.

What looks different.
The live output contains several additional platform-specific host routes (168.63.129.16 and 169.254.169.254) as well as explicit metric tags (metric 100) and protocol details (proto dhcp) that the simplified simulator omitted.

What surprised me.
It was surprising to see specific Azure internal management IP addresses (like the metadata service at 169.254.169.254 and Azure infrastructure host at 168.63.129.16) automatically populated directly in the routing table. Seeing these live cloud provider mechanisms contrasts with the clean, generic networking models used in simulated environments.
```

---

## Part B — The Gateway That Does Not Answer

### Step 1 — Ping the Gateway

Ping the default gateway address you recorded. Let it run a few seconds, then stop it.

Command and output:

```
analyst@cf-student-07:~$ ping 10.60.6.1
PING 10.60.6.1 (10.60.6.1) 56(84) bytes of data.
```

### Step 2 — Interpret It Correctly

You almost certainly got **no replies**. In Azure, the platform gateway commonly does not answer ICMP. This is **expected platform behaviour** and by itself proves nothing about whether your machine or network is broken.

Explain why "the gateway did not answer ping" is weak evidence:

```
A failed ping to the gateway is weak evidence because it confuses a lack of response with a lack of reachability. Many modern cloud environments—such as Azure—deliberately block or drop ICMP Echo Request traffic at the platform level for security, DDoS mitigation, and traffic management purposes. Consequently, the default gateway can be fully operational and actively routing all of your IP traffic while completely ignoring direct ping probes. Relying solely on ICMP failure creates a false positive for network outage when the underlying routing path is actually working normally.
```

---

## Part C — The Known-Good Target

The **Grid Beacon** at `10.60.6.4` is a machine that is known to be up and known to answer. When your first probe fails, you test against something known-good before you conclude anything.

### Step 1 — Ping the Beacon

```
ping 10.60.6.4
```
Output:

```
analyst@cf-student-07:~$ ping 10.60.6.4
PING 10.60.6.4 (10.60.6.4) 56(84) bytes of data.
64 bytes from 10.60.6.4: icmp_seq=1 ttl=64 time=1.35 ms
64 bytes from 10.60.6.4: icmp_seq=2 ttl=64 time=1.19 ms
64 bytes from 10.60.6.4: icmp_seq=3 ttl=64 time=1.16 ms
64 bytes from 10.60.6.4: icmp_seq=4 ttl=64 time=1.18 ms
64 bytes from 10.60.6.4: icmp_seq=5 ttl=64 time=1.15 ms
64 bytes from 10.60.6.4: icmp_seq=6 ttl=64 time=1.15 ms
--- 10.60.6.4 ping statistics ---
277 packets transmitted, 277 received, 0% packet loss, time 276387ms
rtt min/avg/max/mdev = 0.892/1.188/7.243/0.472 ms
```

### Step 2 — Trace the Path

```
traceroute 10.60.6.4
```
Output:

```
analyst@cf-student-07:~$ traceroute 10.60.6.4
traceroute to 10.60.6.4 (10.60.6.4), 30 hops max, 60 byte packets
 1  grid-beacon.internal.cloudapp.net (10.60.6.4)  1.251 ms * *
```

### Step 3 — Ask the Application

```
curl http://10.60.6.4
```
Output:

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GRID BEACON | CVI CyberFoundations</title>
    <style>
        body {
            background: #071426;
            color: #d9f7ef;
            font-family: monospace;
            max-width: 850px;
            margin: 80px auto;
            padding: 30px;
        }
        .beacon {
            border: 1px solid #31d6a6;
            padding: 35px;
        }
        h1 { color: #31d6a6; }
        .label { color: #8ca8ff; }
        .status { color: #31d6a6; }
        .classified {
            margin-top: 30px;
            border-top: 1px solid #31445e;
            padding-top: 20px;
        }
    </style>
</head>
<body>
<div class="beacon">

    <h1>GRID BEACON</h1>

    <p><span class="label">NODE:</span> grid-beacon</p>
    <p><span class="label">NETWORK:</span> CVI Training Grid</p>
    <p><span class="label">STATUS:</span>
       <span class="status">ONLINE</span></p>

    <p>
        Network beacon established.<br>
        If you reached this node, your route is operational.
    </p>

    <div class="classified">
        <p>INVESTIGATION CHECKPOINT</p>

        <p>
            Observe the path that brought you here.
            The destination is only part of the story.
        </p>

        <p>TRACE ID: CF-NET-0604</p>
    </div>

</div>
</body>
</html>
```

> ### ⚠️ Grid Beacon not responding?
> The Grid Beacon is shared course infrastructure and should normally be available. First, confirm your Cloud Heights VM shows **Running** and that you completed the preceding network checks. Then retry the command once after a minute or two.
>
> If the Grid Beacon still does not respond, **stop this part of the lab and contact your instructor.** Record that the shared service was unavailable; do not treat the result as evidence that your VM or your work is incorrect.
>
> Do not change networking, NSGs, firewall rules, routes, DNS, or any Azure settings to try to reach the beacon.
>
> *Instructor note: a confirmed Grid Beacon outage is an environment issue, not a student error. Affected students may complete this portion of Lab 03 after the service is restored, with no penalty.*

### Step 4 — Record the Application Evidence

The beacon returns a banner and a trace ID. Record exactly what you received:

```
GRID BEACON
NODE grid-beacon
NETWORK CVI Training Grid
STATUS ONLINE
Network beacon established.
If you reached this node, your route is open
INVESTIGATION CHECKPOINT
The destination is only part of the story.
TRACE ID
CF-NET-0604 
```

Explain the difference between what the `ping` proved and what the `curl` proved:

```
Ping tests lower-level network reachability, proving only that the destination interface is up, connected, and permitted to respond to echo requests. It does not provide any information about whether specific applications or ports are functioning on the remote machine. Curl tests the full application stack (Layer 7/HTTP over TCP), establishing a three-way TCP handshake and exchanging actual application data. Consequently, a successful ping proves basic network connectivity, while a successful curl proves that the web server software is actively listening, processing requests, and delivering data.
```

### Step 5 — Capture Your Evidence

Two screenshots, both cropped to the terminal only:

**Required filename:** `vm-toolkit-live.png` — your `ip addr` and `ip route` output

**Required filename:** `beacon-reply.png` — your beacon ping/traceroute/curl evidence

---

## Part D — Rewrite the Ladder Rule

Week 5 taught the Ladder Rule: test the near thing before the far thing. Real infrastructure adds a wrinkle — a silent rung is not automatically a broken rung.

Rewrite the Ladder Rule in your own words so that it survives real cloud infrastructure. Your version must include both **route/path evidence** and **a known-good target**:

```
When troubleshooting cloud connectivity, a silent rung is not automatically a broken rung. Before assuming a silent intermediate hop represents a network failure, verify your local configuration using local route/path evidence (such as ip route) and test reachability against a known-good target (such as the Grid Beacon at 10.60.6.4). If traffic successfully traverses the path to reach the known-good destination, the silent device is simply filtering ICMP probes as part of normal platform policy rather than blocking valid network traffic.
```

---

## Analysis Questions

**Analysis Question 1.** Your ping to the gateway failed and your ping to the beacon succeeded. What does that pair of results, taken together, prove about your machine's networking? *(Minimum 3 sentences.)*

```
These two results prove that my computer's network setup and local routing are working completely fine. Since my network traffic had to pass right through the gateway to successfully reach the beacon at 10.60.6.4, the connection outside our local network is clearly up and running. The only thing the failed ping to 10.60.6.1 actually proves is that the gateway is set up to ignore ping requests, not that anything is actually broken.
```

**Analysis Question 2.** Why is `traceroute` useful even when `ping` already answered? What extra thing does it show you? *(Minimum 2 sentences.)*

```
Ping only tells you if the final destination is reachable, traceroute shows you the exact path and every intermediate hop your packets take to get there. This extra path visibility helps you see precisely where latency builds up or where a network route gets delayed or dropped along the way.
```

**Analysis Question 3.** A service is unreachable and ping to it succeeds. Where would you look next, and why is "the network is fine" an incomplete answer? *(Minimum 3 sentences.)*

```
I would check the application layers by looking at the specific port, running services, or local firewalls on the destination host using tools like curl. Stating that "the network is fine" is an incomplete answer because ping only tests basic Layer 3 (IP) connectivity using ICMP packets, completely ignoring higher layers. Even if ICMP traffic gets through, the application service itself could be crashed, listening on the wrong port, or blocked by an OS-level firewall/Network Security Group rule.
```

**Analysis Question 4.** Something already controls what is allowed to reach your machine in Cloud Heights. If you could decide those rules, what would you want to allow, what would you want to block, and who in an organization should get to make that decision? *(Minimum 3 sentences.)*

```
I would want to allow necessary administrative traffic like SSH (port 22) or HTTPS (port 443) only from trusted IP addresses, while blocking all unauthorized, unsolicited incoming connections and unnecessary public ports. This follows the principle of least privilege by ensuring that only essential traffic reaches the system and potential attack surfaces are minimized. Ultimately, security engineering and network administration teams should make these decisions because they understand the organization's overarching security policies, compliance needs, and system dependencies.
```

---

## Submission Checklist

- [x] `ip addr` output recorded and own private IP/prefix identified (Part A)

- [x] `ip route` output recorded and default gateway identified (Part A)

- [x] Live output compared to the Week 5 simulator (Part A, Step 3)

- [x] Gateway pinged and the silent result interpreted correctly (Part B)

- [x] Beacon `ping`, `traceroute`, and `curl` all run and recorded (Part C)

- [x] Beacon banner and TRACE ID recorded (Part C, Step 4)

- [x] `vm-toolkit-live.png` and `beacon-reply.png` captured, cropped, uploaded to `assets/screenshots/week-06/` (Part C, Step 5)

- [x] Ladder Rule rewritten with route evidence + known-good target (Part D)

- [x] All four Analysis Questions answered (minimum sentence counts met)

- [x] This file is committed to your portfolio repo at `week-06/labs/lab-03-the-grid-for-real.md`

---

## GitHub Commit Subsection

1. Open **Week 6 → Lab 03: The Grid, For Real** in the Lab Portal.
2. Fill in the worksheet fields and upload both screenshots to `assets/screenshots/week-06/`.
3. Click **Submit to GitHub** — the Portal commits to `week-06/labs/lab-03-the-grid-for-real.md`.

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
