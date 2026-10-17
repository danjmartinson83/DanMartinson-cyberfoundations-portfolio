# Cloud Heights Family Clinic — Case Packet

Scenario date: Friday 13 March 2026, 09:00 (clinic local time)

A single-location family clinic with 12 staff. It books appointments, keeps patient records, uses staff laptops, publishes a small public information website, and copies its records to a backup drive.

## Clinic facts
- 12 staff: 1 practice manager, 2 clinicians, 3 nurses, 4 reception/scheduling staff, 1 billing clerk, 1 part-time IT contractor (one day a week).
- Appointment system: a hosted scheduling service, signed in with an email address and password. No second step at sign-in.
- Patient records: a records application on the clinic network. Reception staff reach it through one shared account.
- Staff laptops: 9 clinic-owned laptops, managed loosely by the part-time IT contractor.
- Public website: static information pages (address, opening hours, services). It does not contain or reach patient records.
- Backups: one external drive kept plugged into the reception workstation.

## Boundaries of this exercise
- Everything in this case is fictional. No real clinic, patient, address, or mailbox is involved.
- Nothing in this lab scans, connects to, or attacks anything. All output shown is authored teaching text.
- Where a fact is not known, the case says so. Unknown never means 'secure' and never means 'already breached'.

## Assets
### AS-01 — Appointment scheduling account
Books, moves and cancels patient appointments for the whole clinic.
- Confidentiality: The schedule shows who is coming in and when, which is itself information about patients.
- Integrity: Changed or deleted appointments send patients to the wrong place at the wrong time.
- Availability: If reception cannot sign in, the clinic cannot run its day.

### AS-02 — Patient records application
Stores and shows clinical information about patients.
- Confidentiality: Patient information must only be seen by people with a reason.
- Integrity: A wrong or altered record can lead to a wrong clinical decision.
- Availability: Clinicians need the record during the appointment, not later.

### AS-03 — Staff laptops
The devices staff use to reach email and the records application.
- Confidentiality: A laptop signed in and unattended shows whatever is on screen.
- Integrity: Software with known weaknesses can be used to change what runs on the device.
- Availability: A laptop out of action takes a clinician out of action.

### AS-04 — Public information website
Tells the public the address, hours and services of the clinic.
- Confidentiality: Low — the content is meant to be public. The certificate protects the connection, not a secret.
- Integrity: Wrong hours or a wrong phone number sends patients to a closed door.
- Availability: If browsers warn or block visitors, people cannot reliably reach basic clinic information.

### AS-05 — Backup archive
The copy of clinic data used to recover after loss or damage.
- Confidentiality: A backup holds the same sensitive data as the original.
- Integrity: A copy that is incomplete or corrupted restores the wrong thing.
- Availability: Recovery is the whole point: a copy you cannot restore is not recovery.

## Rooms and evidence
### Reception
Books appointments, greets patients, answers the clinic mailbox.
> Priya Osei (Reception & Scheduling Lead): "I had a message this morning saying our scheduling account closes in two hours unless I confirm the password. It looked official, but the address underneath was not our usual one. We get something like this most weeks."

**EV-REC-01 — Email received at the reception mailbox**
- From: Clinic IT Support <appointments@clinic-support.example>
- To: reception@cloudheights-clinic.example
- Received: 13 March 2026, 07:58
- Subject: URGENT — scheduling account will be closed today
- Body: "Our records show your scheduling password has expired. Confirm your username and current password within 2 hours at https://account-verify.clinic-support.example/reset or the appointment system will be locked for your whole clinic today."
- The message is shown here as inert text. The address is not a working link and nothing is sent anywhere.
- Not known: Whether anyone at the clinic replied or entered a password is not recorded anywhere in this case.

**EV-REC-02 — Sender address comparison card**
- The clinic's real scheduling vendor writes from: support@appointments-vendor.example
- The clinic's own domain is: cloudheights-clinic.example
- The message arrived from: clinic-support.example — a third, different domain.
- The display name says "Clinic IT Support". The display name is typed by the sender and is not proof of who sent it.

**EV-REC-03 — Reception desk log note**
- Log note, 13 March 2026: "Third message like this in three weeks. Everyone at the front desk gets them. We just delete them."
- Reception scheduling accounts sign in with an email address and a password only.
- Not known: There is no record of these messages ever being reported to the IT contractor.

### Records Office
Holds the patient records application used across the clinic.
> Renata Coyle (Practice Manager): "All four of my front desk people sign in to records the same way, with the same login. It is quicker. When someone leaves we take their badge back, but that login stays as it is."

**EV-REC-OFF-01 — Records application account list**
- Accounts with access to patient records: 4 clinician/nurse accounts (named), 1 billing account (named), 1 account named `frontdesk`.
- `frontdesk` is the account all four reception staff sign in with. The password is written on a card in the desk drawer.
- Last password change on `frontdesk`: 8 months ago.

**EV-REC-OFF-02 — Records access log extract**
- 12 March 2026 14:02 — user `frontdesk` opened 6 patient records.
- 12 March 2026 16:41 — user `frontdesk` opened 2 patient records.
- Every reception-side entry in the log shows `frontdesk`. The log cannot show which of the four people was at the keyboard.
- Not known: Whether those record openings were appropriate cannot be judged from this log, because the log does not identify a person.

**EV-REC-OFF-03 — Practice manager statement — leavers**
- Renata Coyle, Practice Manager: "When a front desk person leaves we collect their badge. The shared records login stays the same, because changing it means telling everyone the new password."
- Two reception staff have left in the past year.
- Not known: Whether a former member of staff can still reach the records application from outside the clinic is not established by this evidence.

### Staff Workspace
Shared desks where clinicians and nurses use clinic laptops.
> Dev Marchetti (IT Contractor (one day a week)): "Two laptops have not taken security updates in 90 days. Nobody is refusing; they just postpone the restart every day, and no one is responsible for chasing it."

**EV-WKS-01 — Update status report (IT contractor, 13 March 2026)**
- 9 clinic laptops checked.
- 7 laptops: vendor security updates applied within the last 14 days.
- 2 laptops (asset tags CHC-04, CHC-07): no security updates applied for 90 days. Vendor security updates are listed as pending.
- Both pending laptops are used daily for email and for the records application.
- Not known: No alert, no malware detection, and no incident has been reported for these laptops. Missing updates is a weakness, not a confirmed attack.

**EV-WKS-02 — IT contractor statement**
- Dev Marchetti, IT contractor (1 day/week): "Updates need a restart, and those two laptops are in constant use. Staff keep postponing. Nobody owns chasing it."

**EV-WKS-03 — Desk photo — signed-in laptop**
- Photo taken in the shared staff workspace at 09:00: a laptop is signed in to the records application, screen unlocked, no one seated.
- The workspace door opens onto the corridor patients use to reach the waiting area.

### Website Station
Publishes the clinic's public information pages.
> Amara Boateng (Billing Clerk & Website Editor): "I update opening hours on the site. The security certificate gets renewed by hand, usually after someone notices a warning in their browser. It is not on anyone's list."

**EV-WEB-01 — Website certificate details (captured 13 March 2026)**
- Subject: www.cloudheights-clinic.example
- Subject Alternative Name: www.cloudheights-clinic.example, cloudheights-clinic.example
- Issuer: Cloud Heights Teaching CA (fictional issuer used for this lesson)
- Valid from: 20 December 2025, 00:00 UTC
- Valid to: 20 March 2026, 23:59 UTC
- At the scenario date of 13 March 2026 the certificate is valid. It expires in 7 days.

**EV-WEB-02 — Renewal process note**
- Renewal is done by hand. The last two renewals were done by the IT contractor on the day the site started warning visitors.
- There is no calendar reminder and no named owner for renewal in the clinic's records.

**EV-WEB-03 — What the public website actually holds**
- Pages: address and map, opening hours, list of services, a phone number, and a 'how to register' page.
- The website has no sign-in, no patient portal, and no connection to the records application.
- If the certificate expires, visitors' browsers show a warning before the page. The pages themselves are still just public information.
- Not known: A certificate expiring does not, by itself, expose patient records. Those are a separate system.

### Backup Room
Stores the clinic's only copy of its records data.
> Renata Coyle (Practice Manager): "The backup drive stays plugged in so it runs by itself. The last clean run was two weeks ago and we have never tested putting anything back."

**EV-BAK-01 — Backup job history**
- Backup target: one external drive, letter D:, permanently attached to the reception workstation.
- Last successful backup: 27 February 2026 (14 days before the scenario date).
- Since then: 6 job entries reading 'completed with errors — source in use'.
- There are no copies anywhere else: no second drive, no offsite copy, no cloud copy.

**EV-BAK-02 — Restore testing statement**
- Renata Coyle, Practice Manager: "We have never tried to put the data back. We assume it works because the light blinks."
- No restoration test is recorded in any clinic document.
- Not known: Because no restore has ever been attempted, whether the copies would actually work is unknown. Unknown is not the same as broken and not the same as fine.

**EV-BAK-03 — Backup drive photo**
- The drive sits on the desk beside the reception workstation, plugged in by USB, powered on.
- Anything that can write to the reception workstation's files can also write to this drive while it is attached.

## Vocabulary
- **Asset** — Something the clinic needs in order to work, or needs to protect. (An asset is anything of value to the organisation: data, a system, a device, or a service.)
- **Threat / threat event** — The bad thing that could happen, and who or what could cause it. (A threat event is a specific occurrence that could harm an asset, described as actor + action.)
- **Vulnerability** — The weak spot that would let the bad thing happen. (A vulnerability is a weakness in a system, process, or practice that a threat can act on.)
- **Consequence / impact** — What it costs the clinic and its patients if it happens. (Impact is the effect on operations, people, data and obligations if the event occurs.)
- **Likelihood** — How believable it is that this happens here, given what you found. (A qualitative judgement based on exposure, weaknesses present, and protections already in place.)
- **Risk** — The combination of how believable it is and how bad it would be. (Risk here is expressed as a classroom score: likelihood x impact, each rated 1 to 3.)
- **Control** — The thing you change so the bad outcome gets less likely or less painful. (A control is a safeguard applied to reduce likelihood, reduce impact, or improve detection.)
- **Residual risk** — What is still left over after your fix is in place. (The risk remaining once a control is operating. It is described here in words, not invented numbers.)
- **CIA** — Three questions: kept private? correct? available when needed? (Confidentiality, Integrity and Availability.)
- **Attribution** — Being able to say which person did something. (Attribution requires individually identified accounts; shared accounts remove it.)

All content is fictional teaching material. Nothing in this packet was captured from a real system.