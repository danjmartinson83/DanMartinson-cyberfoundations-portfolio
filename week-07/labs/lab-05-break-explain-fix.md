# Week 7 Lab 05 — Break It, Explain It, Fix It

**Student Name:** Dan Martinson

**Date Completed:** 9/6/2026

**Module:** 2 — Networking & Cloud Foundations | **Week:** 7  
**Submission Path:** `week-07/labs/lab-05-break-explain-fix.md`

> ## Cloud Heights Protected-Rules Safety Rule
> Four baseline rules are protected: **100** (`allow-ssh-from-bastion`), **110** (`allow-icmp-intra-vnet`), **120** (`deny-ssh-student-subnet`), and **1000** (`deny-tcp8080-student-subnet` — Inbound Deny TCP from `10.60.6.0/26` to port `8080`). **You never modify, delete, replace, or use a protected rule as a troubleshooting target.** Create or edit student rules only in priorities **200–999**. The priority **1000** fallback deny sits after your band on purpose, so a narrower Allow you create in 200–999 is evaluated first. A mistake in your student range is recoverable and is not a grading penalty when you diagnose it honestly.

> **Evidence safety:** Never include a Cloud Heights password or Bastion shareable URL. Crop browser address bars and login information before committing screenshots.

---

## Mission

Create a controlled priority failure inside your student range, diagnose it from evidence, remove the problem, and retest. The goal is method: UNDERSTAND → PREDICT → CHANGE → TEST → VERIFY, then FORECAST → EXECUTE → VERIFY → REMEDIATE → RETEST.

## What You Already Know

A network security rule is a decision about traffic. Rules are evaluated from the lowest priority number to the highest, and the first matching rule wins. Inbound and outbound traffic use separate ledgers. A configured service, a security rule, a test result, and an evidence screenshot answer different questions.

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Required setup | Lab 03 narrow Allow present; listener running |
| Safe failure | Student-created Deny only; all four protected baselines (100, 110, 120, 1000) untouched |
| Recommended temporary rule | Priority 250 Deny TCP 8080 from `10.60.6.4` |
| Time | 45–55 minutes |

- [x] I am using my assigned `cf-student-XX` VM through the CyberFoundations Lab Portal.

- [x] The VM shows **Running**.

- [x] I can identify the four protected baseline rules at priorities 100, 110, 120, and 1000.

- [x] I understand that my editable priority range is 200–999.

### Cloud Heights Idle Stop

Cloud Heights may warn you that the VM is idle. Return to the Lab Portal and choose **I'm still working** if you are active. If the VM is stopped or deallocated, it was not deleted: restart it from **My Lab Environment**. Your disk files and saved configuration remain.

## UNDERSTAND

Your working Allow is expected at priority 300 or another student value. A new matching Deny with a lower number is evaluated first and makes the later Allow unreachable for that traffic.

## Predict First — FORECAST

Predict Grid Beacon's verdict after adding a priority 250 inbound Deny for TCP 8080 from `10.60.6.4`, while leaving the working Allow in place.

```text
DENIED is my prediction for this test. 
First Matching Rule: deny-grid-beacon-8080-test (Priority 250)
Reason: Security rules evaluate in numerical order from lowest to highest, and the first matching rule wins. Since priority 250 is lower than my working Allow rule at priority 300 (allow-grid-beacon-8080), inbound TCP 8080 traffic from Grid Beacon (10.60.6.4) hits the priority 250 Deny rule first and gets blocked before reaching the Allow rule.
```

## CHANGE / EXECUTE

### Step 1 — Create the Temporary Fault

Create a student rule named `deny-grid-beacon-8080-test`:

- priority `250`
- Inbound / Deny / TCP
- source `10.60.6.4`; source port Any
- destination your assigned VM/default; destination port `8080`
- description: intentional Week 7 troubleshooting fault

Do not edit or delete the Lab 03 Allow. Do not touch the protected priorities 100, 110, 120, or 1000 — the priority 1000 `deny-tcp8080-student-subnet` fallback stays exactly as it is throughout this lab.

### Step 2 — Capture the Broken Ledger

Capture both the priority 250 Deny and the later Allow in the same ordered rule view.

## TEST / VERIFY

Wait at least 10 seconds, select Grid Beacon, and run **Test My Rule**. Expected verdict: `DENIED`.

```text
DENIED

No answer at all from port 8080 before the timeout. Traffic from this source appears to be blocked — a network rule may be denying it, or a higher-priority Deny may be matching first.

Source: Grid Beacon (10.60.6.4) · Port TCP 8080
```

### Stop & Check — Diagnose Before Fixing

Confirm these healthy facts before remediation:

- VM is Running.
- Python listener is still active on 8080.
- The original Allow is still present and correctly scoped.
- The temporary Deny is evaluated first.

```text
Diagnosis:
The connection failure to TCP port 8080 is entirely due to network rule evaluation order, not an infrastructure or service outage.

I confirmed the underlying environment is healthy through the following evidence:
VM Status: The Cloud Heights portal shows cf-student-07 in a Running state.
Service Status: The Python HTTP listener remains active and listening on port 8080 on the target host.
Rule Configuration: The original Lab 03 rule allow-grid-beacon-8080 (Priority 300) is still intact, active, and properly targeted.
Root Cause: Traffic from Grid Beacon (10.60.6.4) matches the newly added deny-grid-beacon-8080-test rule at priority 250 first. Because security rules are processed in numerical order and terminate on the first match, the lower priority number (250) blocks traffic immediately, preventing evaluation from ever reaching the priority 300 Allow rule.
```

## REMEDIATE

Delete only the temporary `deny-grid-beacon-8080-test` rule you created. Removing the controlled fault returns the ledger to the known-good least-privilege state.

## RETEST

1. Wait at least 10 seconds and retest Grid Beacon: expected `ALLOWED`.
2. Wait at least 10 seconds and retest Other Test Source: expected `DENIED`.

```text
ALLOWED

The connection succeeded and your web server answered (HTTP 200\n\n[stderr]\n"}]}). A rule is allowing TCP 8080 from this source.

Source: Grid Beacon (10.60.6.4) · Port TCP 8080

DENIED

No answer at all from port 8080 before the timeout. Traffic from this source appears to be blocked — a network rule may be denying it, or a higher-priority Deny may be matching first.

Source: Other Test Source (10.60.6.10) · Port TCP 8080
```

## Capture Evidence

Your sequence must show broken rules, observed denial, repaired rules, and final retest results.

## Explain — Incident Note

```text
Problem: Inbound traffic on TCP port 8080 from Grid Beacon (10.60.6.4) to my VM (10.60.6.26) was unexpectedly denied despite having a pre-existing allow rule configured.
Evidence: Test My Rule gave a DENIED verdict and timed out when testing traffic from Grid Beacon on port 8080.
Cloud Heights NSG inspection showed the rule deny-grid-beacon-8080-test (Priority 250) positioned above my allow-grid-beacon-8080 rule (Priority 300).
Healthy conditions ruled out: VM Status: VM cf-student-07 was confirmed in a Running state.
Local Service: The Python HTTP server was running and actively listening on port 8080 on the target host.
Allow Rule: The original rule allow-grid-beacon-8080 (Priority 300) remained intact and properly targeted.
Root cause: Network security group rules evaluate sequentially by priority number (lowest value evaluated first) and stop on the first match. Priority 250 (deny-grid-beacon-8080-test) matched inbound traffic from Grid Beacon (10.60.6.4:8080) first, blocking it before evaluation ever reached priority 300 (allow-grid-beacon-8080).
Remediation: Deleted the temporary Priority 250 rule deny-grid-beacon-8080-test from the student priority range.
Retest: Grid Beacon (10.60.6.4): Connection test returned ALLOWED.
Other Test Source (10.60.6.10): Connection test returned DENIED (as expected from the Priority 1000 fallback).
Prevention: Always inspect existing rule priority numbers and evaluation order before creating or troubleshooting security group rules, ensuring allow rules are assigned lower priority numbers (evaluated earlier) than any overlapping deny rules.
```

## Required Evidence

Save screenshots in `assets/screenshots/week-07/`:

- `week07-lab05-broken-rules.png`
- `week07-lab05-observed-denial.png`
- `week07-lab05-fixed-rules.png`
- `week07-lab05-retest-results.png`

Open each image at full size before submission. Confirm that no password, Bastion shareable URL, browser address bar, or unrelated private information is visible.

## Analysis Questions

**Analysis Question 1.** Why did the correct Allow stop working even though it was never edited? (Minimum 4 sentences.)

```text
original allow-grid-beacon-8080 rule stopped taking effect because network security groups process rules sequentially from the lowest priority number to the highest. When the new deny-grid-beacon-8080-test rule was added at Priority 250, it matched the incoming traffic from Grid Beacon (10.60.6.4) on TCP port 8080 before that traffic could reach the Allow rule at Priority 300. Because firewall evaluation immediately terminates once a matching rule is found, the system applied the DENIED verdict from the Priority 250 rule right away. As a result, the intact Allow rule at Priority 300 was completely bypassed and never evaluated, causing legitimate connections to fail despite the Allow rule remaining active and unchanged.
```

**Analysis Question 2.** Why is diagnosing from evaluation order better than changing rules by trial and error? (Minimum 4 sentences.)

```text
Diagnosing from the evaluation order provides a clear, evidence-based understanding of the exact path traffic takes through a firewall, allowing you to identify the root cause immediately rather than guessing. Trial-and-error changes often lead to redundant, overly broad, or misordered rules that can unintentionally weaken overall network security or expose sensitive services to unauthorized traffic. Furthermore, making random rule changes in a live production environment risks causing unexpected downtime for other running applications or locking administrators out of critical systems. Understanding rule priorities and sequential evaluation creates a repeatable, predictable troubleshooting method that allows you to fix issues precisely on the first attempt without introducing new vulnerabilities.
```

**Analysis Question 3.** What made this failure safe and recoverable in the course environment? (Minimum 3 sentences.)

```text
This failure was safe and recoverable because the course environment enforced strict isolation using four protected baseline rules at priorities 100, 110, 120, and 1000 that students could not modify or delete. By restricting all student edits to the 200–999 priority range, critical administrative traffic like SSH access from the Bastion host remained completely protected no matter what changes were made. Additionally, because the failure was caused by a single software-defined security rule, fixing it simply required deleting the temporary priority 250 rule to instantly restore normal traffic flow without risking data loss or permanent system damage.
```

## Submission Checklist

- [x] Forecast written before the change

- [x] Temporary fault stayed in priorities 200–999

- [x] Broken ledger and DENIED result captured

- [x] VM, listener, and original Allow checked before remediation

- [x] Only the temporary Deny removed

- [x] Grid Beacon retested `ALLOWED` and Other Test Source retested `DENIED`

- [x] Incident note completed

- [x] Protected priorities 100, 110, 120, and 1000 were not changed.

- [x] Every rule I created or edited used priority 200–999.

- [x] No password, Bastion URL, or browser address bar appears in my files.

- [x] This worksheet is committed to `week-07/labs/lab-05-break-explain-fix.md`.

## GitHub / Lab Portal Submission

1. Open **Week 7 → Lab 05: Break It, Explain It, Fix It** in the CyberFoundations Lab Portal.
2. Complete every worksheet field and confirm the listed evidence filenames.
3. Upload screenshots to `assets/screenshots/week-07/`.
4. Confirm your portfolio repository is connected, then choose **Submit to GitHub**.
5. Open the committed worksheet and each image on GitHub to verify formatting, legibility, and redaction.

*CyberVisionaries Institute · CyberFoundations · Tier I*
