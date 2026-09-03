# Week 7 Lab 03 — Build the Narrowest Door

**Student Name:** Dan Martinson

**Date Completed:** 8/30/2026

**Module:** 2 — Networking & Cloud Foundations | **Week:** 7  
**Submission Path:** `week-07/labs/lab-03-build-the-narrowest-door.md`

> ## Cloud Heights Protected-Rules Safety Rule
> Four baseline rules are protected: **100** (`allow-ssh-from-bastion`), **110** (`allow-icmp-intra-vnet`), **120** (`deny-ssh-student-subnet`), and **1000** (`deny-tcp8080-student-subnet` — Inbound Deny TCP from `10.60.6.0/26` to port `8080`). **You never modify, delete, replace, or use a protected rule as a troubleshooting target.** Create or edit student rules only in priorities **200–999**. The priority **1000** fallback deny sits after your band on purpose, so a narrower Allow you create in 200–999 is evaluated first. A mistake in your student range is recoverable and is not a grading penalty when you diagnose it honestly.

> **Evidence safety:** Never include a Cloud Heights password or Bastion shareable URL. Crop browser address bars and login information before committing screenshots.

---

## Mission

Run a temporary web service on TCP 8080 and create the least-privilege inbound rule: only Grid Beacon (`10.60.6.4`) may reach the service. You will predict the outcome before changing the ledger and verify the result afterward.

Your Allow at a student priority (recommended `300`) is evaluated **before** the protected priority **1000** `deny-tcp8080-student-subnet` fallback. So before you create the Allow, Grid Beacon's TCP 8080 traffic is denied by that priority 1000 fallback; after your narrow Allow exists and the listener is running, the same traffic is allowed because the lower priority number wins.

## What You Already Know

A network security rule is a decision about traffic. Rules are evaluated from the lowest priority number to the highest, and the first matching rule wins. Inbound and outbound traffic use separate ledgers. A configured service, a security rule, a test result, and an evidence screenshot answer different questions.

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Service command | `python3 -m http.server 8080` |
| Allowed source | Grid Beacon — `10.60.6.4` |
| Test | Portal **Test My Rule**, fixed TCP 8080 |
| Time | 35–45 minutes |

- [x] I am using my assigned `cf-student-XX` VM through the CyberFoundations Lab Portal.

- [x] The VM shows **Running**.

- [x] I can identify the four protected baseline rules at priorities 100, 110, 120, and 1000.

- [x] I understand that my editable priority range is 200–999.

### Cloud Heights Idle Stop

Cloud Heights may warn you that the VM is idle. Return to the Lab Portal and choose **I'm still working** if you are active. If the VM is stopped or deallocated, it was not deleted: restart it from **My Lab Environment**. Your disk files and saved configuration remain.

## Predict First

Before starting the service or creating a rule, predict both conditions:

1. What verdict should Grid Beacon receive while no student Allow exists?
2. What verdict should it receive after the narrow Allow is created and the service is listening?
3. Which rule decides each case — your student Allow, or the protected priority 1000 fallback deny?

```text
1. Verdict while no student Allow exists:
Grid Beacon (10.60.6.4) will receive a DENIED verdict when attempting to connect to TCP port 8080.

2. Verdict after narrow Allow is created and service is listening:
Grid Beacon will receive an ALLOWED verdict once the student Allow rule is created and the Python web service is active and listening on port 8080.

3. Rule decision reasoning:

Before student Allow exists: The protected fallback rule 1000 deny-tcp8080-student-subnet decides the outcome. Because Azure processes rules sequentially from lowest to highest priority number, and no lower-priority rule exists to permit the traffic, it falls through to priority 1000 and gets blocked.

After student Allow exists: The newly created student Allow rule (e.g., priority 300 allow-grid-beacon-8080) decides the outcome. Since priority 300 is evaluated before priority 1000, Azure matches Grid Beacon's IP (10.60.6.4) and destination port (8080) at priority 300, grants access immediately, and stops evaluating further rules.
```

## Guided Steps

### Step 1 — Start the Listener

Open the terminal on your assigned VM and run:

```bash
python3 -m http.server 8080
```

The terminal stays busy while the server runs. Leave it open. `Ctrl+C` stops it when the lab is complete.

### Step 2 — Stop & Check the Service State

Confirm the terminal shows that it is serving on port 8080. If the Portal later reports `SERVICE_NOT_LISTENING`, return here before changing rules.

### Step 3 — Create the Narrow Rule

In Security Rules, add one student rule with these values:

| Field | Required value |
|---|---|
| Name | `allow-grid-beacon-8080` (or a clearly equivalent name) |
| Priority | One unused value from 200–999; recommended `300` |
| Direction | Inbound |
| Action | Allow |
| Protocol | TCP |
| Source | `10.60.6.4` |
| Source port | Any |
| Destination | Your assigned VM / displayed default |
| Destination port | `8080` |
| Description | Week 7 least-privilege test service |

Do not broaden the source to the subnet or Any.

### Step 4 — Record the Change

```text
300
allow-grid-beacon-8080
Direction: Inbound
Protocol: TCP
Port: 8080
Source: 10.60.6.4
Destination: *
Source port: *
```

## Test

Choose **Test My Rule**, select **Grid Beacon (10.60.6.4)**, and run the fixed TCP 8080 test. Wait at least 10 seconds before repeating a test.

Expected verdict: `ALLOWED`.

If you see `SERVICE_NOT_LISTENING`, the rule may be correct but the Python listener is not running. If you see `TEST_ERROR`, verify the VM is running, wait 10 seconds, and retry once before requesting support.

## Capture Evidence

Capture the completed narrow rule and the Grid Beacon `ALLOWED` result. The images must show the source and destination port clearly.

## Explain

Explain why allowing one source to one TCP port is narrower than allowing the whole subnet or Any source, even though all three might make the intended test pass.

```text
Allowing a single source IP (10.60.6.4) to a single TCP port (8080) adheres directly to the principle of least privilege by strictly limiting exposure. While permitting the entire subnet or Any source would satisfy the specific test requirement for Grid Beacon, broad rules unnecessarily expose the web service to every potential actor on the network. If the rule allowed the whole subnet or Any, untrusted or compromised hosts on the network could probe or exploit the open port without triggering a rule block. Specifying exact parameters ensures that only the authorized entity gains access, minimizing the attack surface and maintaining defense-in-depth across the environment.
```

## Required Evidence

Save screenshots in `assets/screenshots/week-07/`:

- `week07-lab03-rule-created.png`
- `week07-lab03-beacon-allowed.png`

Open each image at full size before submission. Confirm that no password, Bastion shareable URL, browser address bar, or unrelated private information is visible.

## Analysis Questions

**Analysis Question 1.** The Python service and the NSG rule perform different jobs. What does each one control? (Minimum 3 sentences.)

```text
The Network Security Group (NSG) rule operates at the network layer to control network access, evaluating inbound traffic to determine whether packets sent to port 8080 are permitted to reach the virtual machine. In contrast, the Python HTTP service operates at the application layer on the host machine, listening on port 8080 to process incoming HTTP requests and send back valid server responses once traffic is allowed through. While the NSG rule acts as a perimeter firewall that grants or blocks network connectivity, the Python service controls the actual host application behavior and response payload once a connection is successfully established.
```

**Analysis Question 2.** Why is `10.60.6.4` a stronger source value than Any for this task? (Minimum 4 sentences.)

```text
Using 10.60.6.4 as the source value is stronger than using Any because it enforces the security principle of least privilege by restricting network access strictly to the single authorized host required for the test. If the source parameter were set to Any, any IP address on the internal subnet or external network could initiate connections to the Python service running on port 8080. This unnecessary exposure increases the system's attack surface, opening up potential opportunities for unauthorized scanning, data interception, or exploitation by untrusted hosts. By explicitly defining 10.60.6.4 (Grid Beacon), the network rule ensures that access is granted solely to the verified testing mechanism while blocking all other potential sources.
```

**Analysis Question 3.** What does an `ALLOWED` result prove, and what does it not prove about other sources? (Minimum 3 sentences.)

```text
ALLOWED result proves that inbound traffic sent specifically from the Grid Beacon IP address (10.60.6.4) to TCP port 8080 successfully matched an active allow rule and reached the running service on the virtual machine. However, it does not prove that other source IP addresses or subnets are permitted, as traffic from different sources may hit higher-priority deny rules or fall through to the baseline fallback rule (1000 deny-tcp8080-student-subnet). Furthermore, testing a single specific source host only validates the network path and policy for that explicit IP, leaving the access state and rule evaluation for all other un-tested network sources unverified.
```

## Submission Checklist

- [x] Listener started before testing

- [x] Narrow inbound Allow created

- [x] Source is exactly `10.60.6.4` and destination port exactly `8080`

- [x] Grid Beacon result is `ALLOWED`

- [x] `week07-lab03-rule-created.png` captured

- [x] `week07-lab03-beacon-allowed.png` captured

- [x] Protected priorities 100, 110, 120, and 1000 were not changed.

- [x] Every rule I created or edited used priority 200–999.

- [x] No password, Bastion URL, or browser address bar appears in my files.

- [x] This worksheet is committed to `week-07/labs/lab-03-build-the-narrowest-door.md`.

## GitHub / Lab Portal Submission

1. Open **Week 7 → Lab 03: Build the Narrowest Door** in the CyberFoundations Lab Portal.
2. Complete every worksheet field and confirm the listed evidence filenames.
3. Upload screenshots to `assets/screenshots/week-07/`.
4. Confirm your portfolio repository is connected, then choose **Submit to GitHub**.
5. Open the committed worksheet and each image on GitHub to verify formatting, legibility, and redaction.

*CyberVisionaries Institute · CyberFoundations · Tier I*
