# Week 7 Lab 01 — Meet the Guard

**Student Name:** Dan Martinson

**Date Completed:** 8/28/2026

**Module:** 2 — Networking & Cloud Foundations | **Week:** 7  
**Submission Path:** `week-07/labs/lab-01-meet-the-guard.md`

> ## Cloud Heights Protected-Rules Safety Rule
> Four baseline rules are protected: **100** (`allow-ssh-from-bastion`), **110** (`allow-icmp-intra-vnet`), **120** (`deny-ssh-student-subnet`), and **1000** (`deny-tcp8080-student-subnet` — Inbound Deny TCP from `10.60.6.0/26` to port `8080`). **You never modify, delete, replace, or use a protected rule as a troubleshooting target.** Create or edit student rules only in priorities **200–999**. The priority **1000** fallback deny sits after your band on purpose, so a narrower Allow you create in 200–999 is evaluated first. A mistake in your student range is recoverable and is not a grading penalty when you diagnose it honestly.

> **Evidence safety:** Never include a Cloud Heights password or Bastion shareable URL. Crop browser address bars and login information before committing screenshots.

---

## Mission

Inspect the existing NIC-level security rules on your assigned VM without changing anything. Your goal is to recognize the guardrails, separate protected rules from student-editable space, and map each visible field to the firewall mental model.

## What You Already Know

A network security rule is a decision about traffic. Rules are evaluated from the lowest priority number to the highest, and the first matching rule wins. Inbound and outbound traffic use separate ledgers. A configured service, a security rule, a test result, and an evidence screenshot answer different questions.

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Environment | My Lab Environment → Cloud Heights → Security Rules |
| Change level | Read-only; do not add, edit, or delete rules |
| Expected protected rules | 100 `allow-ssh-from-bastion`; 110 `allow-icmp-intra-vnet`; 120 `deny-ssh-student-subnet`; 1000 `deny-tcp8080-student-subnet` |
| Time | 15–20 minutes |

- [x] I am using my assigned `cf-student-XX` VM through the CyberFoundations Lab Portal.

- [x] The VM shows **Running**.

- [x] I can identify the four protected baseline rules at priorities 100, 110, 120, and 1000.

- [x] I understand that my editable priority range is 200–999.

### Cloud Heights Idle Stop

Cloud Heights may warn you that the VM is idle. Return to the Lab Portal and choose **I'm still working** if you are active. If the VM is stopped or deallocated, it was not deleted: restart it from **My Lab Environment**. Your disk files and saved configuration remain.

## Predict First

Before opening the rule list, predict why a course environment would protect its access and safety rules from student edits.

```text
A course environment protects its baseline access and safety rules so students don't accidentally cut off administrative connections like SSH and lock themselves out of the virtual machine. Keeping these management rules locked ensures the lab infrastructure stays reachable and functional for everyone. It also creates a safe, isolated priority window where students can experiment with firewall rules without risking permanent damage to the host setup.
```

## Guided Steps

### Step 1 — Open the Guard Post

Start your VM from **My Lab Environment** first. The **Live Azure lab** card is only a launcher — all rule work happens in the Lab Portal's **Security Rules** panel. Do not work in the Azure Portal.

In Cloud Heights, scroll **below** the yellow *Protected rules — do not modify* summary to the detailed list headed **INBOUND — EVALUATION ORDER**. That detailed list, not the yellow summary, is what you inventory and capture.

### Step 2 — Inventory the Baseline

Record each protected rule exactly as shown.

| Priority | Rule name | Direction | Protocol | Source | Destination/port | Action | Protected? |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 100 | allow-ssh-from-bastion | Inbound | Tcp | 192.168.10.128/26 | 22 | Allow | Yes |
| 110 | allow-icmp-intra-vnet | Inbound | icmp |  VirtualNetwork | * | Allow | Yes |
| 120 | deny-ssh-student-subnet | inbound | Tcp | 10.60.6.0/26 | 22 | Deny | Yes |
| 1000 | deny-tcp8080-student-subnet | Inbound | Tcp | 10.60.6.0/26 | 8080 | Deny | Yes |

### Step 3 — Map the Fields

For each field, write the question it answers: direction, source, source port, destination, destination port, protocol, action, and priority.

```text
allow-ssh-from-bastion is priority 100 and pretty important; the direction is inbound from source 192.168.10.128/26 to destination port 22 using the Transmission Control Protocol.  The action is allowed and protected.

allow-icmp-intra-vnet is priority 110, still very high on the rulebook. The direction is inbound with a Internet Control Message Protocol. The source is the source VirtualNetwork with an unknown destination port.  The action allowed and protected.

deny-ssh-student-subnet is priority 120 the direction is inbound using the Transmission Control Protocol. The source is 10.60.6.0/26 and destination is port 22.  The action is denied and protected.

deny-tcp8080-student-subnet is priority 1000 and inbound.  The protocol is Transmission Control Protocol from the source 10.60.6.0/26 to the destination port 8080. The action is denied and protected.   
```

## Stop & Check

- Can you edit a protected rule? You should not be able to — all four are locked.
- Where may student rules be created? Priorities 200–999.
- Which value is read first: 200 or 900? The lower number, 200.

## Test

This is a read-only lab: do not add, edit, or delete any rule. Your test is visual verification — confirm all four protected rules remain present and that no student rule was created.

## Capture Evidence

Capture the detailed **INBOUND — EVALUATION ORDER** view showing all four protected rules (100, 110, 120, 1000) and no student rule. If it does not fit in one image, use two clearly named images and explain why.

## Explain

In 3–4 sentences, explain how protected baselines and a separate student priority band reduce accidental lockout while still allowing meaningful practice.

```text
Protected baseline rules sit at the highest priority levels to lock down critical admin access like SSH, ensuring we can't accidentally lock ourselves out while working. Restricting our edits to a separate student priority band (200–999) gives us a safe sandbox to add, test, and troubleshoot custom rules without destroying those essential management connections. Because student rules evaluate right after the baselines but before the fallback deny rules, we get to see realistic firewall behavior and learn from our mistakes without breaking the whole lab setup.
```

## Required Evidence

Save screenshots in `assets/screenshots/week-07/`:

- `week07-lab01-security-rules-baseline.png`

Open each image at full size before submission. Confirm that no password, Bastion shareable URL, browser address bar, or unrelated private information is visible.

## Analysis Questions

**Analysis Question 1.** Why is a priority number part of rule behavior rather than just an identifier? (Minimum 3 sentences.)

```text
A priority number actively dictates the evaluation order because firewalls process rules sequentially from the lowest number to the highest. Since the firewall stops inspecting the moment traffic matches a rule "first match wins", a lower priority number gives a rule higher precedence over others. If it were just an identifier, the system wouldn't know which rule to apply when network traffic matches multiple overlapping criteria, like an allow rule and a deny rule.
```

**Analysis Question 2.** Explain the difference between a rule being visible, editable, and protected. (Minimum 3 sentences.)

```text
A rule being visible means it shows up in our evaluation list so we can review its priority, settings, and how it handles traffic. A rule being editable means we have permission to change its parameters—like modifying ports, source IPs, or priority numbers—or delete it completely, which applies to any rules we create in the student range (200–999). Finally, a rule being protected means it's locked down by the lab environment (like rules 100, 110, 120, and 1000) so we can't alter or delete it, keeping essential baseline security and access controls safely intact while we practice.
```

**Analysis Question 3.** Which baseline rule protects your current administrative path, and why must it never be used as a troubleshooting target? (Minimum 3 sentences.)

```text
The baseline rule that protects our administrative path is priority 100, allow-ssh-from-bastion, which permits inbound SSH traffic on port 22 from the Bastion host subnet (192.168.10.128/26). We can never use this rule as a troubleshooting target because messing with or trying to override it would cut off our SSH session and completely lock us out of the VM. Since it's a locked baseline put in place to maintain management access, any rule creation, testing, or troubleshooting we do has to stay strictly inside our designated student band (priorities 200–999).
```

## Submission Checklist

- [x] Baseline inventory completed without changes

- [x] All visible rule fields mapped to their security questions

- [x] Editable range 200–999 identified

- [x] `week07-lab01-security-rules-baseline.png` captured

- [x] Protected priorities 100, 110, 120, and 1000 were not changed.

- [x] I did not create, edit, or delete any security rules during this read-only lab.

- [x] No password, Bastion URL, or browser address bar appears in my files.

- [x] This worksheet is committed to `week-07/labs/lab-01-meet-the-guard.md`.

## GitHub / Lab Portal Submission

1. Open **Week 7 → Lab 01: Meet the Guard** in the CyberFoundations Lab Portal.
2. Complete every worksheet field and confirm the listed evidence filenames.
3. Upload screenshots to `assets/screenshots/week-07/`.
4. Confirm your portfolio repository is connected, then choose **Submit to GitHub**.
5. Open the committed worksheet and each image on GitHub to verify formatting, legibility, and redaction.

*CyberVisionaries Institute · CyberFoundations · Tier I*
