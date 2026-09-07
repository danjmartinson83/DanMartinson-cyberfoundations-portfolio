# Week 7 Lab 04 — Prove the Guard Works ★ Deliverable 2

**Student Name:** Dan Martinson

**Date Completed:** 9/2/2026

**Module:** 2 — Networking & Cloud Foundations | **Week:** 7  
**Submission Path:** `week-07/labs/lab-04-prove-the-guard-works.md`

> ## Cloud Heights Protected-Rules Safety Rule
> Four baseline rules are protected: **100** (`allow-ssh-from-bastion`), **110** (`allow-icmp-intra-vnet`), **120** (`deny-ssh-student-subnet`), and **1000** (`deny-tcp8080-student-subnet` — Inbound Deny TCP from `10.60.6.0/26` to port `8080`). **You never modify, delete, replace, or use a protected rule as a troubleshooting target.** Create or edit student rules only in priorities **200–999**. The priority **1000** fallback deny sits after your band on purpose, so a narrower Allow you create in 200–999 is evaluated first. A mistake in your student range is recoverable and is not a grading penalty when you diagnose it honestly.

> **Evidence safety:** Never include a Cloud Heights password or Bastion shareable URL. Crop browser address bars and login information before committing screenshots.

---

## Mission

Assemble Deliverable 2 evidence by proving both halves of least privilege: the intended source is allowed and an unintended source is denied. A single successful test is not enough.

## What You Already Know

A network security rule is a decision about traffic. Rules are evaluated from the lowest priority number to the highest, and the first matching rule wins. Inbound and outbound traffic use separate ledgers. A configured service, a security rule, a test result, and an evidence screenshot answer different questions.

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Required setup | Lab 03 rule present; Python listener still running |
| Allowed source | Grid Beacon — `10.60.6.4` |
| Unintended source | Other Test Source — `10.60.6.10` |
| Deliverable | Security group configuration + verification evidence |
| Time | 30–40 minutes |

- [x] I am using my assigned `cf-student-XX` VM through the CyberFoundations Lab Portal.

- [x] The VM shows **Running**.

- [x] I can identify the four protected baseline rules at priorities 100, 110, 120, and 1000.

- [x] I understand that my editable priority range is 200–999.

### Cloud Heights Idle Stop

Cloud Heights may warn you that the VM is idle. Return to the Lab Portal and choose **I'm still working** if you are active. If the VM is stopped or deallocated, it was not deleted: restart it from **My Lab Environment**. Your disk files and saved configuration remain.

## Predict First

**Prerequisite from Lab 03 (required):** the Python listener is running on TCP 8080, and your narrow inbound Allow for `10.60.6.4` port `8080` exists in priorities **200–999**. If either is missing, finish Lab 03 first.

**Expected results:** Grid Beacon `10.60.6.4` is **ALLOWED** by your student Allow; Other Test Source `10.60.6.10` is **DENIED** by the protected priority **1000** `deny-tcp8080-student-subnet` fallback.

**DO NOT** create an additional deny rule, broaden your allow, or modify any protected rule to produce these results.

Without changing the Lab 03 rule, predict the result from each test source.

| Source | Prediction | Deciding rule/reason |
| --- | --- | --- |
| Grid Beacon `10.60.6.4` | ALLOWED | Student rule 300 allow-grid-beacon-8080. Evaluated first (priority 300 < 1000), matching source IP 10.60.6.4 and port 8080. |
| Other Test Source `10.60.6.10` | DENIED | Protected rule 1000 deny-tcp8080-student-subnet. Falls through rule 300 (does not match 10.60.6.10), hitting the priority 1000 subnet-wide fallback deny for 10.60.6.0/26. |

## Guided Steps

### Step 1 — Verify the Final Configuration

Confirm the listener is running and the student Allow remains inbound TCP 8080 from exactly `10.60.6.4`.

### Step 2 — Test the Intended Source

Select **Grid Beacon (10.60.6.4)** and run **Test My Rule**. Record the verdict and compare it with your prediction.

```text
ALLOWED
The result matches my prediction. When testing from Grid Beacon (10.60.6.4), the inbound request on TCP port 8080 matched my custom student rule 300 allow-grid-beacon-8080. Because Azure evaluates network security group rules sequentially by priority and priority 300 is lower than the protected priority 1000 fallback deny rule, the traffic was permitted immediately upon matching rule 300.
```

### Step 3 — Test the Unintended Source

Wait at least 10 seconds. Select **Other Test Source (10.60.6.10)** and run the same fixed TCP 8080 test.

```text
DENIED
The result matches my prediction. When testing from the unintended source (10.60.6.10), the inbound request on TCP port 8080 did not match the student rule 300 allow-grid-beacon-8080 because the source IP did not match 10.60.6.4. Azure continued evaluating rules sequentially until it hit the protected baseline rule 1000 deny-tcp8080-student-subnet. Because rule 1000 blocks TCP port 8080 for the entire 10.60.6.0/26 subnet, traffic from 10.60.6.10 was denied.
```

Expected verdict: `DENIED`, produced by the protected priority 1000 fallback.

If either result differs from expected, **stop making changes**: capture the complete rule list in evaluation order plus the test result, and report it to your instructor in this worksheet. Do not add a deny rule, broaden the allow, or modify protected rules.

## Stop & Check

Your evidence pair should now prove:

- the intended connection is permitted;
- the unintended connection is not permitted;
- the service was listening during both tests;
- the rule source is narrow rather than Any.

## Test Summary

| Evidence question | Result |
| --- | --- |
| Is the service listening? | Yes (Python HTTP service active on port 8080) |
| Is Grid Beacon allowed? | Yes (ALLOWED verdict verified) |
| Is Other Test Source denied? | Yes (DENIED verdict verified) |
| Which rule produces the intended Allow? | 300 allow-grid-beacon-8080 |

## Capture Evidence

Capture the final rule plus both result cards. Screenshots must show the selected source and verdict. These images are the core evidence for Deliverable 2.

## Explain — Deliverable 2 Statement

Write a concise professional statement covering what you configured, the source/port scope, the two tests, and how the results prove least privilege.

```text
To enforce least-privilege network access, I configured an inbound Network Security Group rule (300 allow-grid-beacon-8080) that permits TCP traffic on destination port 8080 restricted strictly to a single source IP address, Grid Beacon (10.60.6.4). Verification was performed while a Python HTTP service was active and listening on port 8080 on my target virtual machine (10.60.6.26).
During testing, the authorized Grid Beacon source yielded an ALLOWED verdict because its traffic matched rule 300 before reaching lower-priority rules. Conversely, testing from an unauthorized host (10.60.6.10) yielded a DENIED verdict, falling through rule 300 and hitting the fallback rule 1000 deny-tcp8080-student-subnet. Together, these paired test results demonstrate least privilege by confirming that network access is granted exclusively to the required host while all other subnet traffic remains explicitly blocked.
```

## Required Evidence

Save screenshots in `assets/screenshots/week-07/`:

- `week07-lab04-final-rule.png`
- `week07-lab04-grid-beacon-allowed.png`
- `week07-lab04-other-source-denied.png`

Open each image at full size before submission. Confirm that no password, Bastion shareable URL, browser address bar, or unrelated private information is visible.

## Analysis Questions

**Analysis Question 1.** Why are one ALLOWED result and one DENIED result stronger evidence together than either result alone? (Minimum 4 sentences.)

```text
Having both an ALLOWED result and a DENIED result together provides stronger evidence because it proves both positive access for authorized traffic and effective restriction against unauthorized traffic. An ALLOWED result alone only confirms that a path exists for the intended host, but it fails to demonstrate whether the security rule is overly permissive (such as allowing the entire subnet or Any source). Conversely, a DENIED result alone only shows that traffic was blocked, which could simply indicate a broken network connection, an inactive service, or a blanket block-all rule rather than intentional security controls. Combining both outcomes verifies the boundaries of least privilege by demonstrating that access is granted selectively to the exact permitted source while active controls simultaneously block unintended hosts.
```

**Analysis Question 2.** If the Other Test Source were ALLOWED, what would you inspect before changing anything? (Minimum 4 sentences.)

```text
If the Other Test Source were unexpectedly ALLOWED, I would first inspect the active inbound Network Security Group rules in priority evaluation order (from lowest to highest priority number) to identify which specific rule matched the traffic. Next, I would examine the source field of my student rule (300 allow-grid-beacon-8080) to confirm whether it was accidentally configured with a broad scope like Any or a subnet CIDR range (10.60.6.0/26) instead of the exact single IP (10.60.6.4). I would also check for any additional, higher-priority custom or default allow rules (priority values below 1000) that might permit TCP port 8080 traffic across the broader VNet. Finally, I would verify the destination and port parameters of all preceding rules to ensure no overlapping allow rule was inadvertently granting access before the packet reached the protected priority 1000 fallback deny.
```

**Analysis Question 3.** How does this evidence distinguish configuration from observed enforcement? (Minimum 3 sentences.)

```text
Static configuration only shows intent by defining desired rule parameters (such as setting an allowed IP, port, and priority in the Network Security Group table), but it cannot guarantee that traffic will flow or be blocked as expected. Live test results provide observed enforcement, proving that the network stack and underlying firewall rules actually process active packets according to those static definitions. By capturing both the configured rule set and the resulting ALLOWED and DENIED test verdicts, this evidence proves that the intended security policy is actively enforced at runtime rather than existing merely as an unverified setting on paper.
```

## Submission Checklist

- [x] Final rule screenshot shows narrow source and TCP 8080

- [x] Grid Beacon `ALLOWED` evidence captured

- [x] Other Test Source `DENIED` evidence captured

- [x] Deliverable 2 statement completed

- [x] `week07-lab04-final-rule.png` captured

- [x] `week07-lab04-grid-beacon-allowed.png` captured

- [x] `week07-lab04-other-source-denied.png` captured

- [x] Protected priorities 100, 110, 120, and 1000 were not changed.

- [x] Every rule I created or edited used priority 200–999.

- [x] No password, Bastion URL, or browser address bar appears in my files.

- [x] This worksheet is committed to `week-07/labs/lab-04-prove-the-guard-works.md`.

## GitHub / Lab Portal Submission

1. Open **Week 7 → Lab 04: Prove the Guard Works ★ Deliverable 2** in the CyberFoundations Lab Portal.
2. Complete every worksheet field and confirm the listed evidence filenames.
3. Upload screenshots to `assets/screenshots/week-07/`.
4. Confirm your portfolio repository is connected, then choose **Submit to GitHub**.
5. Open the committed worksheet and each image on GitHub to verify formatting, legibility, and redaction.

*CyberVisionaries Institute · CyberFoundations · Tier I*
