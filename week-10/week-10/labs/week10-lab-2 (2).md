# Week 10 — Lab 2: Prioritize Risks and Recommend Controls

Learner: Dan Martinson
Case: Cloud Heights Family Clinic — Risk & Threat Investigation
Scenario date: Friday 13 March 2026, 09:00 (clinic local time)
Report generated: 2026-10-17T22:59:27.186Z
Study mode: Guided (hints available)

Completion checklist: all required work for Lab 2 is present.

## Risk ratings

| ID | Asset | Likelihood | Why | Impact | Why | Score (L x I) | Classroom band |
| --- | --- | --- | --- | --- | --- | --- | --- |
| SC-01 | Appointment scheduling account | 3 | As documented in EV\-REC\-01 and EV\-REC\-03, front desk staff receive fraudulent urgency phishing messages "most weeks" from lookalike domains, and reception accounts rely solely on single\-factor credentials \(email and password\) without multi\-factor authentication. | 3 | If credentials are compromised or accounts locked out, daily clinic appointments cannot be booked, rescheduled, or managed, causing a total halt to clinic operations. | 9 | High (6–9) |
| SC-02 | Patient records application | 3 | EV\-REC\-OFF\-01 shows that all four receptionists share a single generic account \(frontdesk\) with the password written on a physical card in the desk drawer, and EV\-REC\-OFF\-03 confirms credentials are never rotated when staff leave. | 3 | Compromise or unauthorized access exposes sensitive patient clinical records for the entire clinic, resulting in a severe confidentiality breach and complete loss of individual accountability. | 9 | High (6–9) |
| SC-03 | Staff laptops | 2 | EV\-WKS\-01 and EV\-WKS\-02 show laptops running 90 days behind on updates due to constant postponements, and EV\-WKS\-03 documents a terminal left signed in and unlocked right next to a patient corridor. | 2 | Physical or remote exposure affects specific workstation data and terminal integrity, though recovery and containment can be managed locally without halting the entire clinic. | 4 | Medium (3–4) |
| SC-04 | Public information website | 2 | EV\-WEB\-01 and EV\-WEB\-02 establish that TLS certificate renewals are handled entirely manually and reactively, with no calendar tracking and an expiration date only 7 days away. | 1 | The public website contains only general information \(hours, map, services\) and has no connection to patient records \(EV\-WEB\-03\), so an expiration only causes public navigation friction rather than operational shutdown or data loss. | 2 | Low (1–2) |
| SC-05 | Backup archive | 3 | EV\-BAK\-01 and EV\-BAK\-03 confirm the backup drive is permanently plugged in via USB \(exposed to live malware modification\) and its last six backup runs completed with errors. | 3 | If a ransomware attack or hardware failure occurs, the clinic faces catastrophic, unrecoverable data loss because backups have never been tested \(EV\-BAK\-02\). | 9 | High (6–9) |

Bands (1–2 low, 3–4 medium, 6–9 high) are a classroom teaching aid, not a compliance standard.

## Priority risks
- SC-01 — Appointment scheduling account
- SC-02 — Patient records application

**Why these:** Risk 1 and Risk 2 represent the clinic's highest-scoring \(9/9\) and most actively targeted assets. The appointment scheduling account faces weekly phishing pressure \(EV-REC-01\) targeting single-factor credentials, creating a constant frontline exposure that could halt daily operations. Meanwhile, the patient records application suffers from critical internal vulnerabilities—including shared credentials \(frontdesk\), passwords stored on cards in desk drawers \(EV-REC-OFF-01\), and unrotated passwords after staff departures \(EV-REC-OFF-03\)—threatening patient privacy and accountability. Addressing these two first secures both our primary external threat entry point and our most sensitive internal data repository.

## Recommended controls
### SC-01
- **Control:** Enable multi-factor authentication \(MFA\) for the reception scheduling account and establish a formal reporting channel so staff can notify IT of incoming phishing attempts.
- **How it helps:** It makes the threat event significantly less damaging and harder to exploit. Even if front-desk staff are deceived by a phishing email and enter their credentials into a lookalike domain, the attacker cannot access the scheduling system without the mandatory second factor \(such as an app-based code or hardware token\).
- **Risk remaining afterwards:** Phishing emails will still arrive in the reception inbox \(EV-REC-01\), and staff could theoretically be manipulated into approving an MFA push prompt if heavily targeted. However, the risk of a successful credential-harvesting takeover resulting from a single leaked password is substantially reduced.

### SC-02
- **Control:** Transition from the shared frontdesk account \(EV-REC-OFF-01\) to individual, named user accounts for all four reception staff members, remove the written password card from the desk drawer, and enforce immediate password deactivation or rotation upon staff departures.
- **How it helps:** It directly closes the shared-account and un-rotated credential vulnerabilities. By issuing individual logins, the clinic restores accountability and non-repudiation, ensuring every entry in the access logs \(EV-REC-OFF-02\) ties directly to a specific person rather than a generic group account.
- **Risk remaining afterwards:** Individual staff members could still write down their personal passwords or leave terminals unattended if behavioral habits are not enforced, meaning internal misuse or accidental disclosure via desk notes remains a minor residual risk.

## Owner briefing
Word count: 125 (guide: 100–150)

Dear Renata,

Following our security review of Cloud Heights Family Clinic, we identified two critical areas needing immediate attention: our appointment scheduling account security and our patient records access control.

Currently, reception staff face weekly phishing attempts targeting single-factor scheduling logins \(EV-REC-01\), and all four receptionists share a single frontdesk record account with a password stored on a desk drawer card \(EV-REC-OFF-01\). This leaves us vulnerable to account takeover and prevents us from tracking individual record access \(EV-REC-OFF-02\).

We recommend implementing multi-factor authentication for scheduling logins and migrating to individual, named user accounts for patient records while removing stored password cards. While these steps will not stop phishing attempts entirely or eliminate all endpoint risks, they directly secure our core operational workflows and patient data.
