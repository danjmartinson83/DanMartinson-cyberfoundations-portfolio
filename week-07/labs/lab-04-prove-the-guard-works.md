# Week 7 Lab 04 — Prove the Guard Works ★ Deliverable 2

**Student Name:**  
**Date Completed:**  
**Module:** 2 — Networking & Cloud Foundations | **Week:** 7  
**Submission Path:** `week-07/labs/lab-04-prove-the-guard-works.md`

> ## Cloud Heights Protected-Rules Safety Rule
> The baseline rules at priorities **100** (`allow-ssh-from-bastion`), **110** (`allow-icmp-intra-vnet`), and **120** (`deny-ssh-student-subnet`) are protected. **Never modify, delete, replace, or use them as troubleshooting targets.** Create or edit student rules only in priorities **200–999**. A mistake in your student range is recoverable and is not a grading penalty when you diagnose it honestly.

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

- [ ] I am using my assigned `cf-student-XX` VM through the CyberFoundations Lab Portal.
- [ ] The VM shows **Running**.
- [ ] I can identify the three protected baseline rules at priorities 100, 110, and 120.
- [ ] I understand that my editable priority range is 200–999.

### Cloud Heights Idle Stop

Cloud Heights may warn you that the VM is idle. Return to the Lab Portal and choose **I'm still working** if you are active. If the VM is stopped or deallocated, it was not deleted: restart it from **My Lab Environment**. Your disk files and saved configuration remain.

## Predict First

Without changing the Lab 03 rule, predict the result from each test source.

| Source | Prediction | Deciding rule/reason |
|---|---|---|
| Grid Beacon `10.60.6.4` |  |  |
| Other Test Source `10.60.6.10` |  |  |

## Guided Steps

### Step 1 — Verify the Final Configuration

Confirm the listener is running and the student Allow remains inbound TCP 8080 from exactly `10.60.6.4`.

### Step 2 — Test the Intended Source

Select **Grid Beacon (10.60.6.4)** and run **Test My Rule**. Record the verdict and compare it with your prediction.

```text
(record verdict and explanation here)
```

### Step 3 — Test the Unintended Source

Wait at least 10 seconds. Select **Other Test Source (10.60.6.10)** and run the same fixed TCP 8080 test.

```text
(record verdict and explanation here)
```

Expected verdict: `DENIED`. If it is `ALLOWED`, stop and inspect all student rules in evaluation order. Do not change protected rules.

## Stop & Check

Your evidence pair should now prove:

- the intended connection is permitted;
- the unintended connection is not permitted;
- the service was listening during both tests;
- the rule source is narrow rather than Any.

## Test Summary

| Evidence question | Result |
|---|---|
| Is the service listening? |  |
| Is Grid Beacon allowed? |  |
| Is Other Test Source denied? |  |
| Which rule produces the intended Allow? |  |

## Capture Evidence

Capture the final rule plus both result cards. Screenshots must show the selected source and verdict. These images are the core evidence for Deliverable 2.

## Explain — Deliverable 2 Statement

Write a concise professional statement covering what you configured, the source/port scope, the two tests, and how the results prove least privilege.

```text
(your Deliverable 2 statement here — 5 to 7 sentences)
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
(your answer here)
```

**Analysis Question 2.** If the Other Test Source were ALLOWED, what would you inspect before changing anything? (Minimum 4 sentences.)

```text
(your answer here)
```

**Analysis Question 3.** How does this evidence distinguish configuration from observed enforcement? (Minimum 3 sentences.)

```text
(your answer here)
```

## Submission Checklist

- [ ] Final rule screenshot shows narrow source and TCP 8080
- [ ] Grid Beacon `ALLOWED` evidence captured
- [ ] Other Test Source `DENIED` evidence captured
- [ ] Deliverable 2 statement completed
- [ ] `week07-lab04-final-rule.png` captured
- [ ] `week07-lab04-grid-beacon-allowed.png` captured
- [ ] `week07-lab04-other-source-denied.png` captured
- [ ] Protected priorities 100, 110, and 120 were not changed.
- [ ] Every rule I created or edited used priority 200–999.
- [ ] No password, Bastion URL, or browser address bar appears in my files.
- [ ] This worksheet is committed to `week-07/labs/lab-04-prove-the-guard-works.md`.

## GitHub / Lab Portal Submission

1. Open **Week 7 → Lab 04: Prove the Guard Works ★ Deliverable 2** in the CyberFoundations Lab Portal.
2. Complete every worksheet field and confirm the listed evidence filenames.
3. Upload screenshots to `assets/screenshots/week-07/`.
4. Confirm your portfolio repository is connected, then choose **Submit to GitHub**.
5. Open the committed worksheet and each image on GitHub to verify formatting, legibility, and redaction.

*CyberVisionaries Institute · CyberFoundations · Tier I*
