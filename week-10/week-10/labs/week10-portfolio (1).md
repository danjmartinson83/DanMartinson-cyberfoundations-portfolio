# Week 10 — Cloud Heights Family Clinic: Full Portfolio Report

This report combines Lab 1 and Lab 2. It contains only your own work.

All Week 10 requirements are present, including all five room visits.

---

# Week 10 — Lab 1: Investigate What Needs Protection

Learner: Dan Martinson
Case: Cloud Heights Family Clinic — Risk & Threat Investigation
Scenario date: Friday 13 March 2026, 09:00 (clinic local time)
Report generated: 2026-10-17T23:02:12.351Z
Study mode: Independent (hints hidden)

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

Lack of Accountability / Non-Repudiation Failure: Because everyone uses the same login, access logs only record front desk and cannot prove which individual was actually at the keyboard \(EV-REC-OFF-02\). Furthermore, when staff leave, the shared password is kept the same to avoid inconvenience \(EV-REC-OFF-03\).

3. What would it cost the clinic if something went wrong?
Loss of Accountability: If a data breach, unauthorized access, or policy violation occurs, the clinic cannot determine who was responsible, complicating internal investigations or regulatory reporting.

Unauthorized Access Retention: Former employees who left within the past year still potentially know the un-rotated shared password, giving them ongoing access to sensitive patient records.

4. What do we still not know? \(Unknowns\)
Appropriateness of Access: Whether the record openings logged on 12 March 2026 were appropriate or authorized cannot be judged, as the log fails to identify the specific staff member \(EV-REC-OFF-02\).

External Access by Leavers: Whether a former staff member can still reach the records application from outside the clinic is not established by the evidence \(EV-REC-OFF-03\).

1. What is worth protecting here?The Patient Records Application \(AS-02\): This system stores sensitive clinical information, patient histories, and medical records for the entire clinic, requiring strict confidentiality and integrity.2. What weakness can I actually see in the evidence?Shared User Account: All four reception staff sign in to the records system using a single shared account \(frontdesk\) rather than individual accounts \(EV-REC-OFF-01\).Insecure Credential Storage: The password for the shared account is physically written down on a card stored right in the desk drawer \(EV-REC-OFF-01\).Stale Credentials: The shared password has not been changed in 8 months \(EV-REC-OFF-01\).Lack of Accountability \(Non-Repudiation Failure\): Because everyone logs in under the same name, access logs only show frontdesk and cannot prove which individual staff member was actually at the keyboard \(EV-REC-OFF-02\).Failure to Rotate Passwords on Staff Departure: When reception staff leave, the shared password is kept the same to avoid the inconvenience of telling everyone a new one, despite two staff members having left in the past year \(EV-REC-OFF-03\).   3. What would it cost the clinic if something went wrong?   Loss of Accountability: If a data breach, unauthorized access, or policy violation occurs, the clinic cannot determine who was responsible, complicating internal reviews, accountability, and regulatory compliance.   Persistent Unauthorized Access: Former employees who left within the past year still potentially know the unchanged shared password, giving them ongoing access to sensitive patient records from outside or inside the clinic.4. What do we still not know? \(Unknowns\)Appropriateness of Record Access: Whether the specific record openings logged on 12 March 2026 were appropriate or authorized cannot be judged, because the log fails to identify an individual person \(EV-REC-OFF-02\).External Access by Leavers: Whether a former member of staff can still reach the records application from outside the clinic is not established by the evidence \(EV-REC-OFF-03\).

Room 3: Staff Workspace using the three core investigation questions, ensuring your findings clearly separate proven weaknesses from what remains unknown:

1. What is worth protecting here?
Staff Laptops \(AS-03\): The daily endpoint devices used by staff to access both clinic email and the patient records application.

Active Record Sessions: The confidentiality of open, signed-in applications left running on unattended physical terminals.

2. What weakness can I actually see in the evidence?
Prolonged Unpatched Vulnerabilities: Two clinic laptops \(CHC-04 and CHC-07\) have gone 90 days without vendor security updates because staff constantly postpone necessary reboots during daily use \(EV-WKS-01, EV-WKS-02\).

Lack of Accountability / Governance: There is no assigned ownership or enforcement mechanism to ensure updates are actually applied \(EV-WKS-02\).

Physical Security Exposure: A clinic laptop was left signed in with an active, unlocked records session while completely unattended, positioned next to a doorway opening directly onto a patient-accessible corridor \(EV-WKS-03\).

3. What would it cost the clinic if something went wrong?
Unauthorized Physical Access: Anyone walking down the patient corridor could easily enter the workspace and view, modify, or steal patient data from an unprotected, active session \(EV-WKS-03\).

Endpoint Compromise: Leaving endpoints 90 days behind on security patches increases their susceptibility to remote exploitation via email or network vectors \(EV-WKS-01\).

4. What do we still not know? \(Unknowns\)
Absence of Incidents / Active Attacks: As explicitly noted in EV-WKS-01, missing updates and an unlocked screen represent structural weaknesses, but there are no alerts, malware detections, or indications that an actual security breach has occurred on these laptops.
Room 4: Website Station using your three core investigation questions, based on the evidence cards \(EV-WEB-01, EV-WEB-02, and EV-WEB-03\):

1. What is worth protecting here?
The Public Information Website \(AS-04\): The clinic's digital shop window \(www.cloudheights-clinic.example\) that provides patients with essential details like the clinic address, map, opening hours, services, phone number, and registration instructions.

Website Trust and Accessibility: Ensuring visitors can access the public site without being blocked or frightened away by security warnings.

2. What weakness can I actually see in the evidence?
Manual, Reactive Renewal Process: The website TLS/SSL security certificate is renewed entirely by hand with no automated tracking \(EV-WEB-01, EV-WEB-02\).

Lack of Accountability and Oversight: There is no calendar reminder and no named owner for certificate renewal anywhere in the clinic's records \(EV-WEB-02\). Consequently, renewals historically only happen reactively—specifically on the exact day visitors start seeing browser warning errors \(EV-WEB-02\).

Upcoming Expiration Risk: The active certificate expires in just 7 days \(on 20 March 2026\), sitting on a ticking clock with no internal tracking \(EV-WEB-01\).

3. What would it cost the clinic if something went wrong?
Public Distrust and Confusion: If the certificate expires, visitors' browsers will display a prominent security warning before allowing them to view the site \(EV-WEB-03\). This makes the clinic look unprofessional, causes frustration, and may deter patients from seeking contact details or opening hours.

Administrative Friction: Staff or the IT contractor will have to scramble to perform an emergency manual renewal once complaints or warnings start rolling in \(EV-WEB-02\).

4. What do we still not know? \(Unknowns\)
Separation from Sensitive Systems: As explicitly highlighted in EV-WEB-03, a certificate expiring or a website compromise does not expose patient records, because the public website has no sign-in, no patient portal, and is completely disconnected from the internal records application.

Room 5 \(Backup Room\) using your three core investigation questions, based on the evidence cards \(EV-BAK-01, EV-BAK-02, and EV-BAK-03\):

1. What is worth protecting here?
The Backup Archive \(AS-05\): The clinic’s sole fallback copy of critical data, which is required to recover systems and patient records after data loss, hardware failure, or destructive incidents.

2. What weakness can I actually see in the evidence?
Stale and Failing Backups: The last successful backup was on 27 February 2026 \(14 days prior\), and the subsequent 6 backup attempts have all completed with errors \(source in use\) \(EV-BAK-01\).

Single Point of Failure / Lack of Redundancy: There are no other copies anywhere else—no second drive, no offsite copy, and no cloud copy \(EV-BAK-01\).

Always-Connected Vulnerability: The external backup drive is permanently plugged in via USB and powered on right beside the reception workstation, meaning any malware or unauthorized process that can write to the workstation's files can also instantly corrupt or delete the backup data \(EV-BAK-01, EV-BAK-03\).

Untested Restoration Process: The clinic has never attempted to actually restore data from the drive, relying entirely on assumption rather than proof \(EV-BAK-02\).

3. What would it cost the clinic if something went wrong?
Catastrophic Data Loss: If the primary clinic data or workstation were corrupted, encrypted by ransomware, or physically damaged, the clinic would discover that their backup archive is outdated, incomplete \(completed with errors\), and potentially impossible to restore, leading to total loss of critical clinic and patient records.

4. What do we still not know? \(Unknowns\)
Whether the Backups Actually Work: As EV-BAK-02 explicitly notes, because no restore has ever been attempted, whether the backup copies would successfully recover data is entirely unknown. \(As emphasized: unknown is not the same as broken, but it is not the same as fine\).




Scenario 1: Appointment Scheduling Account \(SC-01\)
Evidence Attached: EV-REC-01, EV-REC-02, EV-REC-03

Threat / Event: An external threat actor launches a credential-harvesting phishing campaign targeting front desk staff using spoofed IT notices to trick employees into revealing their scheduling account credentials.

Vulnerability: Reception scheduling accounts rely solely on a single factor \(email and password\) with no MFA, and staff face constant phishing pressure \(most weeks\) without formal reporting channels to IT.

Consequence: If credentials are compromised, unauthorized actors could lock out, view, or alter clinic appointments, halting daily clinic operations.

CIA Concern: Availability and Confidentiality \(disruption of booking systems and potential exposure of scheduling workflows\).

Scenario 2: Patient Records Application \(SC-02\)
Evidence Attached: EV-REC-OFF-01, EV-REC-OFF-02, EV-REC-OFF-03

Threat / Event: An unauthorized individual \(such as an internal actor or a former employee who left within the past year\) accesses sensitive patient clinical data.

Vulnerability: All four receptionists share a single generic account \(frontdesk\) with an un-rotated password written on a physical card in the desk drawer, violating non-repudiation and leaving old credentials active after staff departures.

Consequence: Total loss of accountability where individual actions cannot be traced, and lingering access for departed personnel.

CIA Concern: Confidentiality and Accountability / Integrity.

Scenario 3: Staff Laptops \(SC-03\)
Threat / Event: An attacker or unauthorized visitor exploits unpatched operating system vulnerabilities or accesses an active session on an unattended device.

Vulnerability: Two daily-use laptops \(CHC-04 and CHC-07\) are 90 days behind on security updates due to constant deferrals and lack of ownership, and physical terminals are left signed in and unlocked right next to patient-accessible corridors.

Consequence: Endpoint compromise via remote exploitation or direct physical data exfiltration/tampering by patients or visitors walking down the corridor.

CIA Concern: Confidentiality and Integrity.

Scenario 4: Public Information Website \(SC-04\)
Threat / Event: Visitors encounter browser security warnings or the clinic's public-facing presence becomes untrusted due to an expired TLS certificate.

Vulnerability: Manual, reactive renewal processes with no calendar tracking or named owner, resulting in certificates running right up to expiration deadlines.

Consequence: Public trust degradation and administrative scramble when visitors are blocked by browser warnings trying to view operating hours or address details.

CIA Concern: Availability \(trust/accessibility of public info\).

Scenario 5: Backup Archive \(SC-05\)
Threat / Event: A major system failure, hardware crash, or ransomware attack occurs, and the clinic attempts to recover data from its backup archive.

Vulnerability: The single external backup drive is permanently plugged in via USB \(making it vulnerable to simultaneous corruption by malware\) and has failed its last six runs \(completed with errors\), with zero restoration tests ever performed.

Consequence: Catastrophic data loss and inability to recover clinic records, as the backup is outdated, unverified, and potentially corrupt.

CIA Concern: Availability and Integrity.


Scenario 1 \(SC-01\): Appointment Scheduling Account
Asset: AS-01 — Appointment scheduling account

Evidence I am using: \[x\] EV-REC-01, \[x\] EV-REC-02, \[x\] EV-REC-03

Threat / event: An external threat actor sends a phishing email mimicking IT support to trick reception staff into entering their credentials on a lookalike domain page.

Vulnerability: Reception scheduling accounts rely solely on an email and password with no multi-factor authentication, and staff face constant phishing pressure \(most weeks\) without formal reporting channels.

Consequence: If credentials are compromised or accounts locked out, the clinic cannot book, reschedule, or manage patient appointments for the day, halting operations.

CIA concern\(s\): Confidentiality, Availability

Unknown / question: Whether anyone at the clinic actually replied to the messages or entered their password is not recorded anywhere.

Scenario 2 \(SC-02\): Patient Records Application
Asset: AS-02 — Patient records application

Evidence I am using: \[x\] EV-REC-OFF-01, \[x\] EV-REC-OFF-02, \[x\] EV-REC-OFF-03

Threat / event: An unauthorized individual \(such as an internal actor or a former employee who left within the past year\) accesses sensitive patient clinical records.

Vulnerability: All four receptionists share a single generic account \(frontdesk\) with an unrotated password written on a physical card in the desk drawer, violating non-repudiation.

Consequence: Total loss of accountability where individual actions cannot be traced, and lingering access for departed personnel.

CIA concern\(s\): Confidentiality, Integrity

Unknown / question: Whether record openings logged on 12 March 2026 were appropriate cannot be judged, and whether former staff can reach the system externally is unknown.

Scenario 3 \(SC-03\): Staff Laptops
Asset: AS-03 — Staff laptops

Evidence I am using: \[x\] EV-WKS-01, \[x\] EV-WKS-02, \[x\] EV-WKS-03

Threat / event: An unauthorized visitor walking down the patient corridor steps into the shared workspace and views or alters data on an unattended, unlocked laptop.

Vulnerability: Staff leave active records sessions running on unlocked terminals right next to a doorway opening directly onto a patient corridor, and devices are running 90 days behind on patches due to a lack of update ownership.

Consequence: Direct physical data exposure/tampering or remote exploitation of unpatched vulnerabilities.

CIA concern\(s\): Confidentiality, Integrity

Unknown / question: While missing updates and unlocked screens are confirmed weaknesses, no malware detection or active attack has been reported for these laptops.

Scenario 4 \(SC-04\): Public Information Website
Asset: AS-04 — Public information website

Evidence I am using: \[x\] EV-WEB-01, \[x\] EV-WEB-02, \[x\] EV-WEB-03

Threat / event: Public visitors are blocked or frightened away from viewing clinic opening hours and contact details when their browsers display security warnings.

Vulnerability: The website TLS certificate has a manual, reactive renewal process with no calendar reminder or named owner, letting it run right up to its expiration date.

Consequence: Public trust degradation, patient confusion, and an administrative scramble for emergency manual renewals.

CIA concern\(s\): Availability

Unknown / question: An expiring certificate does not expose patient records, as the public website is completely disconnected from internal records.

Scenario 5 \(SC-05\): Backup Archive
Asset: AS-05 — Backup archive

Evidence I am using: \[x\] EV-BAK-01, \[x\] EV-BAK-02, \[x\] EV-BAK-03

Threat / event: A major system crash or ransomware attack occurs, and the clinic discovers it cannot successfully recover its data from the backup archive.

Vulnerability: The external backup drive is permanently plugged in via USB \(exposing it to simultaneous malware modification\) and its last six backup jobs completed with errors, with zero restoration tests ever performed.

Consequence: Catastrophic data loss and permanent inability to recover critical clinic records.

CIA concern\(s\): Availability, Integrity

Unknown / question: Because no restore has ever been attempted, whether the backup copies would actually work is completely unknown.

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


---

# Week 10 — Lab 2: Prioritize Risks and Recommend Controls

Learner: Dan Martinson
Case: Cloud Heights Family Clinic — Risk & Threat Investigation
Scenario date: Friday 13 March 2026, 09:00 (clinic local time)
Report generated: 2026-10-17T23:02:12.351Z
Study mode: Independent (hints hidden)

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

