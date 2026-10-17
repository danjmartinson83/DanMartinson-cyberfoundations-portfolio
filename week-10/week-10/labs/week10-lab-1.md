# Week 10 — Lab 1: Investigate What Needs Protection

Learner: Dan Martinson
Case: Cloud Heights Family Clinic — Risk & Threat Investigation
Scenario date: Friday 13 March 2026, 09:00 (clinic local time)
Report generated: 2026-10-17T22:16:03.487Z
Study mode: Guided (hints available)

Completion checklist: all required work for Lab 1 is present.

## Evidence added to my findings
- EV-REC-01 — Email received at the reception mailbox
- EV-REC-02 — Sender address comparison card
- EV-REC-03 — Reception desk log note
- EV-REC-OFF-01 — Records application account list
- EV-REC-OFF-02 — Records access log extract
- EV-REC-OFF-03 — Practice manager statement — leavers
- EV-WKS-03 — Desk photo — signed-in laptop
- EV-WKS-02 — IT contractor statement
- EV-WKS-01 — Update status report (IT contractor, 13 March 2026)
- EV-WEB-03 — What the public website actually holds
- EV-WEB-02 — Renewal process note
- EV-WEB-01 — Website certificate details (captured 13 March 2026)
- EV-BAK-03 — Backup drive photo
- EV-BAK-02 — Restore testing statement
- EV-BAK-01 — Backup job history

## My investigation notebook
1. What is worth protecting here?
The Appointment Scheduling Account \(AS-01\): This system controls booking, moving, and canceling patient appointments for the entire clinic. If compromised or locked out, daily clinic operations and patient care scheduling halt completely.

Front Desk Credentials: The credentials \(email and password\) used by reception staff to access the scheduling system.

2. What weakness can I actually see in the evidence?
Credential-Only Authentication: According to EV-REC-03, reception scheduling accounts sign in with just an email address and a password, with no multi-factor authentication \(MFA\) mentioned, making them highly vulnerable to credential theft or phishing attacks.

High Phishing Exposure & Habituation: Staff receive these fraudulent urgency messages "most weeks" \(EV-REC-01 and EV-REC-03\), leading to normalization of deviance where staff just delete them without formally reporting them to IT contractors.

Spoofable Sender/Context: The attacker uses a lookalike domain \(clinic-support.example\) mimicking IT support with a false sense of urgency \("closes in two hours"\) to manipulate staff into bypassing security hygiene.

3. What would it cost the clinic if something went wrong?
Operational Disruption: If an attacker successfully gains access or locks out the system, the clinic cannot book, reschedule, or manage patient appointments for the entire day.

Reputational and Patient Trust Damage: Disrupted appointments lead to frustrated patients, delayed medical care, and potential exposure or manipulation of operational workflows.

4. What questions do you still have?
Did anyone fall for it? As noted in EV-REC-01, there is no record anywhere in the case of whether any staff member ever replied or entered their password into these fake links.

Is there a reporting mechanism? EV-REC-03 highlights that there is no record of these phishing emails ever being officially reported to the IT contractor, meaning IT has no visibility into ongoing targeting campaigns.

1. What is worth protecting here?
The Appointment Scheduling Account \(AS-01\): This system controls all patient bookings, modifications, and cancellations across the clinic. If compromised or locked out, daily operations grind to a halt.

Front Desk Credentials: The email address and password combinations used by reception staff to access the scheduling infrastructure.

2. What weakness can I actually see in the evidence?
Credential-Only Authentication: As noted in EV-REC-03, reception accounts sign in with just an email and password, lacking multi-factor authentication \(MFA\) to prevent unauthorized access if credentials are leaked or phished.

High Phishing Exposure and Normalization: Staff receive these fraudulent urgency messages "most weeks" \(EV-REC-01 and EV-REC-03\), leading to a dangerous habituation where staff simply delete them without formally reporting them to IT.

Spoofable Sender Context: Attackers leverage lookalike domains \(clinic-support.example\) and false authority \("Clinic IT Support"\) coupled with artificial urgency \("closes in two hours"\) to manipulate staff behavior.

3. What would it cost the clinic if something went wrong?
Operational Paralysis: An attacker locking out or taking over the scheduling system means the clinic cannot book, reschedule, or manage patient visits for the entire day.

Patient Trust and Clinical Impact: Disrupted schedules lead to delayed medical care, missed appointments, and degraded patient trust in the clinic's administrative safety.

4. What do we still not know? \(Unknowns\)
Whether anyone fell for it: EV-REC-01 explicitly notes that whether anyone at the clinic replied or entered a password is not recorded anywhere.

Whether IT was ever notified: EV-REC-03 highlights that there is no record of these phishing attempts ever being reported to the IT contractor, meaning IT lacks visibility into the ongoing campaign targeting the front desk.

Records Office, which covers the patient records application \(AS-02\) and its associated vulnerabilities.
1. What is worth protecting here?
The Patient Records Application \(AS-02\): This system stores sensitive clinical information and patient records for the entire clinic, requiring strict confidentiality, integrity, and non-repudiation.

2. What weakness can I actually see in the evidence?
Shared Account \(frontdesk\): All four reception staff share a single login account \(frontdesk\) rather than having individual accounts \(EV-REC-OFF-01\).

Insecure Credential Storage: The password for the shared account is physically written down on a card in the desk drawer \(EV-REC-OFF-01\).

Stale Credentials: The password has not been changed in 8 months \(EV-REC-OFF-01\).

Lack of Accountability / Non-Repudiation Failure: Because everyone uses the same login, access logs only record frontdesk and cannot prove which individual was actually at the keyboard \(EV-REC-OFF-02\). Furthermore, when staff leave, the shared password is kept the same to avoid inconvenience \(EV-REC-OFF-03\).

3. What would it cost the clinic if something went wrong?
Loss of Accountability: If a data breach, unauthorized access, or policy violation occurs, the clinic cannot determine who was responsible, complicating internal investigations or regulatory reporting.

Unauthorized Access Retention: Former employees who left within the past year still potentially know the un-rotated shared password, giving them ongoing access to sensitive patient records.

4. What do we still not know? \(Unknowns\)
Appropriateness of Access: Whether the record openings logged on 12 March 2026 were appropriate or authorized cannot be judged, as the log fails to identify the specific staff member \(EV-REC-OFF-02\).

External Access by Leavers: Whether a former staff member can still reach the records application from outside the clinic is not established by the evidence \(EV-REC-OFF-03\).

## Risk scenarios

| ID | Asset | Evidence | Threat / event | Vulnerability | Consequence | CIA | Unknown / question |
| --- | --- | --- | --- | --- | --- | --- | --- |
| SC-01 | Appointment scheduling account | EV\-REC\-01 \(Email received at the reception mailbox\); EV\-REC\-02 \(Sender address comparison card\); EV\-REC\-03 \(Reception desk log note\) | An external threat actor sends a phishing email mimicking IT support to trick reception staff into entering their credentials on a lookalike domain page. | Reception scheduling accounts rely solely on a single factor \(email and password\) with no multi\-factor authentication, and staff face constant phishing pressure \(most weeks\) without formal reporting channels. | If credentials are compromised or accounts locked out, the clinic cannot book, reschedule, or manage patient appointments for the day, halting clinic operations. | Confidentiality, Availability | Whether anyone at the clinic actually replied to the messages or entered their password is not recorded anywhere. |
| SC-02 | Patient records application | EV\-REC\-OFF\-01 \(Records application account list\); EV\-REC\-OFF\-02 \(Records access log extract\); EV\-REC\-OFF\-03 \(Practice manager statement — leavers\) | An unauthorized individual \(such as an internal actor or a former employee who left within the past year\) accesses sensitive patient clinical records. | All four receptionists share a single generic account \(frontdesk\) with an un\-rotated password written on a physical card in the desk drawer, violating non\-repudiation. | Total loss of accountability where individual actions cannot be traced, and lingering access for departed personnel. | Confidentiality, Integrity | Whether record openings logged on 12 March 2026 were appropriate cannot be judged, and whether former staff can reach the system externally is unknown. |
| SC-03 | Staff laptops | EV\-WKS\-01 \(Update status report \(IT contractor, 13 March 2026\)\); EV\-WKS\-02 \(IT contractor statement\); EV\-WKS\-03 \(Desk photo — signed\-in laptop\) | An unauthorized visitor walking down the patient corridor steps into the shared workspace and views or alters data on an unattended, unlocked laptop. | Staff leave active records sessions running on unlocked terminals right next to a doorway opening directly onto a patient corridor, and devices are running 90 days behind on patches due to a lack of update ownership. | Direct physical data exposure/tampering or remote exploitation of unpatched vulnerabilities. | Confidentiality, Integrity | While missing updates and unlocked screens are confirmed weaknesses, no malware detection or active attack has been reported for these laptops. |
| SC-04 | Public information website | EV\-WEB\-01 \(Website certificate details \(captured 13 March 2026\)\); EV\-WEB\-02 \(Renewal process note\); EV\-WEB\-03 \(What the public website actually holds\) | Public visitors are blocked or frightened away from viewing clinic opening hours and contact details when their browsers display security warnings. | The external backup drive is permanently plugged in via USB \(exposing it to simultaneous malware modification\) and its last six backup jobs completed with errors, with zero restoration tests ever performed. | Catastrophic data loss and permanent inability to recover critical clinic records. | Availability | Because no restore has ever been attempted, whether the backup copies would actually work is completely unknown. |
| SC-05 | Backup archive | EV\-BAK\-01 \(Backup job history\); EV\-BAK\-02 \(Restore testing statement\); EV\-BAK\-03 \(Backup drive photo\) | A major system crash or ransomware attack occurs, and the clinic discovers it cannot successfully recover its data from the backup archive. | The external backup drive is permanently plugged in via USB \(exposing it to simultaneous malware modification\) and its last six backup jobs completed with errors, with zero restoration tests ever performed. | Catastrophic data loss and permanent inability to recover critical clinic records. | Integrity, Availability | Because no restore has ever been attempted, whether the backup copies would actually work is completely unknown. |

## Email analysis
1. The sender address \(appointments@clinic-support.example\) does not match the clinic's real scheduling vendor \(support@appointments-vendor.example\) or the clinic's own domain \(cloudheights-clinic.example\).
2. Artificial urgency and pressure tactics \("closes in two hours", "system will be locked for your whole clinic today"\) intended to bypass critical thinking.
3. The link points to an external lookalike subdomain \(account-verify.clinic-support.example/reset\) rather than the official vendor portal.

**Safe response / reporting step:** Do not click the link or enter any credentials. Delete the email and officially log/report the phishing attempt to the IT contractor \(Dev Marchetti\) or Practice Manager \(Renata Coyle\).

**Suspicious vs proven:** This message proves that external actors are actively sending phishing emails attempting to spoof IT support and harvest credentials. However, it does not prove whether any staff member clicked the link, replied, or had their account compromised.
