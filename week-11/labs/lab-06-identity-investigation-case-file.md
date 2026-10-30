# Lab 06 — Identity Investigation + Case File (Deliverable 4)

**Learner:** Dan Martinson  
**Attempt:** attempt 81B676 · seed chic-w11-v1 · state revision 202 · text revision 137

> Training simulation — fictional Cloud Heights accounts and resources. Your actions change only your Week 11 learning attempt. This is not a live AD domain, Microsoft Entra tenant or Azure subscription.

## Objective

Correlate historical logs and assemble the Cloud Heights IAM Investigation Case File — Portfolio Deliverable 4.

## My answers

### Starting hypothesis before filtering

Initial review of the September 21 historical sign-in records suggests a mix of routine user authentication errors and potential credential guessing attempts (such as multiple failed password attempts on specific accounts followed eventually by success). These records will need to be cross-referenced against the audit logs using correlation IDs to determine whether authentication anomalies align with any administrative configuration changes or group modifications.

## IAM Investigation Case File (Portfolio Deliverable 4)

_This is a technical case file. Week 12 uses it as source material to produce the professional Technical Incident Report and Executive Summary and to finalize and present the portfolio._

### 1. Scope and environment

This investigation examined identity access management, administrative controls, and sign-in activities across the simulated Cloud Heights Identity Center environment. The scope was limited to the fictional Week 11 training simulation datasets, audit logs, and directory structures, without affecting external live domains or production resources.

### 2. Identity/directory trace and AD DS–Entra–Azure comparison

In this environment, the relationship between human users, assigned digital accounts, directory groups, and role-based permissions connects simulated Active Directory domain services with cloud identity contexts. Specifically, individuals authenticate via directory accounts mapped to organizational security groups, which in turn inherit granular access rights and resource permissions across the simulated infrastructure similar to how on-premises AD objects bridge with cloud tenants.

### 3. Blair authentication-versus-authorization investigation

The sign-in and access records show that successful authentication (signing in) only verifies a user's identity, whereas resource authorization requires explicit group memberships, permissions, or access grants. Specifically, while Blair successfully authenticated to the environment, access to restricted resources remained governed by whether authorized group memberships and policy grants were actively assigned.

### 4. Directory administration and sensitive-action verification

During directory administration, I performed simulated user provisioning, group modifications, and sensitive-action verifications under proper change approvals and identity checks, ensuring all administrative actions were properly logged and tracked against corresponding tickets.

### 5. Three job-role configurations, scopes and business rationales

The role configuration was scoped to restrict access permissions based strictly on functional requirements, adhering to the principle of least privilege by ensuring that each role grants only the minimum necessary rights required to perform designated tasks without over-provisioning access across the simulated environment.

### 6. Access test matrix and temporary grant/revoke evidence

I tested access by evaluating various user privileges against targeted resources within the access matrix, verifying that temporary grants functioned correctly during active windows and were successfully removed upon expiration as reflected in the audit evidence logs.

### 7. ABAC current-policy and what-if findings

The current-policy test showed that access controls successfully enforced active attribute-based access control rules, while subsequent what-if tests simulated alternative policy states to demonstrate how attribute modifications would alter access permissions without committing permanent changes to the environment.

### 8. Joiner/mover/leaver and unverified-reset decisions

For the lifecycle requests, I checked corresponding identity records, administrative tickets, and authorization logs to ensure joiner provisions, mover transitions, and leaver revocations were executed with valid approvals and proper verification steps.

### 9. Historical identity findings (see findings below)

My historical findings are supported by the selected event IDs and associated metadata, which trace the timeline of authentication attempts, administrative ticket changes, and session continuations across the historical record.

#### Finding 1: Casey Account Compromise and Privilege Escalation

- **Events:** S004, S005, S006, S007, S008, S009
- **Observation:** The records show multiple consecutive failed password attempts for the user casey@cvi-training.example from an unknown device at a remote location (IP 203.0.113.77) between 14:00:00 and 14:02:00 UTC, culminating in a successful authentication without an MFA challenge at 14:03:00 UTC, followed immediately by an audit log entry showing the account added itself to the Privileged-Operators group with no approval ticket recorded.
- **Hypothesis:** One possible explanation is that an attacker used credential guessing against the user account casey@cvi-training.example from an unknown remote device until gaining access, and then immediately abused that access to self-assign membership to the Privileged-Operators group.
- **Supported conclusion:** Based on the available records, we can support that user account casey@cvi-training.example experienced multiple consecutive failed password attempts originating from an unknown remote device (203.0.113.77) followed by a successful authentication without an MFA challenge, which directly correlated with a subsequent audit log entry showing the account successfully adding itself to the Privileged-Operators group with no approval ticket recorded.
- **Uncertainty / missing information:** The available evidence does not establish whether the brute-force attempts and subsequent unauthorized group addition were performed by an external malicious actor using compromised credentials or by an insider operating the device.
- **Next action:** Next, we should check active session tokens and recent account activity for the affected user to determine if unauthorized access persists, and immediately review the group membership change to revoke any unauthorized privileges granted.
- **Priority:** high — This priority is reasonable because an unauthorized account compromise followed by immediate self-assignment to a privileged group grants an attacker high-level access to sensitive systems and data, creating an immediate risk of widespread compromise or data exfiltration.

#### Finding 2: Blair Account Access and Authorized Group Addition

- **Events:** S001, S002, S003, S010, S011, A001, A002, A003, A004
- **Observation:** The records show that user blair@cvi-training.example experienced an incorrect password attempt at 13:01 UTC followed by a successful authentication at 13:02 UTC from a managed device, and a subsequent audit entry at 13:10 UTC confirming helpdesk added Blair to the Junior-Analysts group under approval ticket CHG-1101.
- **Hypothesis:** One possible explanation is that the user blair@cvi-training.example made a simple typo when entering their password on their managed device before successfully authenticating, and subsequently had their group membership provisioned legitimately through standard change management procedures (CHG-1101).
- **Supported conclusion:** Based on the available records, we can support that user blair@cvi-training.example successfully authenticated after an initial password error, and that their subsequent addition to the Junior-Analysts group was properly authorized and logged under change control ticket CHG-1101.
- **Uncertainty / missing information:** The available evidence does not establish the reason behind the initial sign-in password error or whether any informal communications preceded the official helpdesk change ticket.
- **Next action:** No further operational action is required for this finding, as the group membership addition was properly authenticated, verified, and executed via a legitimate change management ticket (CHG-1101).
- **Priority:** low — This priority is reasonable because the activity followed legitimate change management controls (CHG-1101) and did not represent an unauthorized security risk or operational threat.

#### Finding 3: 

- **Events:** none
- **Observation:** _Not written yet._
- **Hypothesis:** _Not written yet._
- **Supported conclusion:** _Not written yet._
- **Uncertainty / missing information:** _Not written yet._
- **Next action:** _Not written yet._
- **Priority:** not set — _Not written yet._

### 10. Sign-in/audit correlation and one benign/ambiguous comparison

The selected records are linked by shared user identities, timestamps, and correlation keys that connect authentication sign-in events directly to downstream audit actions. Furthermore, benign and ambiguous records—such as minor password retries followed by successful authentication or IP shifts during active sessions—demonstrate normal user behavior and should not be misconstrued as compromise without explicit evidence of malicious intent.

**Benign/ambiguous comparison** (S010, S011, S002, S003): Initially, the sudden change in IP addresses and locations across Alex's session records (S010 and S011) might look concerning or resemble session hijacking or impossible travel, while Blair's record (S002) featuring an incorrect password attempt prior to success (S003) could initially resemble a brute-force or credential-stuffing attempt. However, another reasonable explanation is that Alex simply moved locations or switched networks while maintaining an existing, valid authenticated session (existing_session, satisfied_earlier), and Blair simply made a minor typing error before successfully authenticating on a managed device. Therefore, we should not overclaim malicious activity, compromise, or unauthorized access because the authentication metadata explicitly indicates normal session persistence and routine user error rather than malicious pivoting or successful brute-force exploitation.

**Live simulator chain (current attempt, not historical):** During my Week 11 work, I performed an audit evidence export test to verify reporting controls. Record LA-81B676-193-2 shows that the action was successfully processed and recorded by the simulator.

### 11. Preliminary response/remediation recommendations, priority and uncertainty

The next action I recommend checking is validating recent helpdesk ticket closure verification steps and prioritizing any ambiguous sign-in retries with low urgency, while acknowledging that the exact motivation behind user typing errors remains uncertain due to limited historical telemetry.

### 12. Evidence index notes

This Case File references event IDs S002, S003, S010, and S011 to trace authentication attempts, password error states, and session persistence across historical sign-in and audit logs.

### Explicit simulation/environment limitations

This investigation is limited by the boundaries of a fictional training simulation, missing contextual telemetry regarding off-network user behavior, and the inability to independently verify unconfirmed human factors or external motivations behind routine administrative and user actions.

### Earlier labs

- [Lab 01](lab-01-identity-directory.md)
- [Lab 02](lab-02-authentication-vs-authorization.md)
- [Lab 03](lab-03-build-and-manage-directory.md)
- [Lab 04](lab-04-least-privilege-challenge.md)
- [Lab 05](lab-05-joiner-mover-leaver.md)

## Evidence

- **E17 · EV-81B676-025** — Two distinct findings with raw-event references and correlation (captured at revision 193)  
  _What this proves:_ These records support my observation that historical sign-in and audit events exhibit correlated administrative actions and session continuations across distinct timestamps. Their correlation shows temporal relationships between authentication attempts and group modifications, but does not establish the underlying intent or external human factors behind those events.  
  See [evidence index](evidence/week11-evidence-index.md#ev-81b676-025)
- **E18 · EV-81B676-026** — Benign/ambiguous comparison (captured at revision 193)  
  _What this proves:_ These records show an initial authentication failure due to an incorrect password followed immediately by a successful sign-in attempt. The information is limited because it captures only authentication outcomes without providing context on whether the initial failure was a simple typographical error or indicative of suspicious activity.  
  See [evidence index](evidence/week11-evidence-index.md#ev-81b676-026)
- **E17 · EV-81B676-027** — Two distinct findings with raw-event references and correlation (captured at revision 202)  
  _What this proves:_ These records support my observation that multiple failed authentication attempts preceded a successful sign-in on the target account. Their correlation shows event sequencing and administrative changes, but does not establish user intent.  
  See [evidence index](evidence/week11-evidence-index.md#ev-81b676-027)
- **E19 · EV-81B676-028** — Completed case file / versioned export (captured at revision 202)  
  _What this proves:_ My downloaded Case File references these records to support the analysis of authentication anomalies and administrative group modifications.  
  See [evidence index](evidence/week11-evidence-index.md#ev-81b676-028)
