# Cloud Heights Identity Investigation — Technical Incident Report

> Fictional training scenario: Cloud Heights Identity Center (simulated). No real organisation, people or systems.

- Analyst: Dan Martinson
- Source case file: [../week-11/labs/lab-06-identity-investigation-case-file.md](../week-11/labs/lab-06-identity-investigation-case-file.md)
- Evidence index: [../week-11/labs/evidence/week11-evidence-index.md](../week-11/labs/evidence/week11-evidence-index.md)

## 1. Purpose / incident context
This report documents the investigation of suspicious authentication and access events associated with user account casey@cvi-training.example, triggered by multiple consecutive failed password attempts originating from unknown remote IP address 203.0.113.77 between 14:00:00 and 14:02:00 UTC, followed immediately by an unauthorized self-assignment to the Privileged-Operators group at 14:03:00 UTC.

## 2. Scope
The investigation covered user account casey@cvi-training.example, the authentication logs, audit records, and group membership changes associated with the Privileged-Operators group during the incident window between 14:00:00 and 14:03:00 UTC. It did not cover broader tenant-wide directory access logs, unrelated user accounts, or active sessions outside of the specified event window.

## 3. Evidence reviewed
The following records were reviewed: sign-in logs showing authentication attempts from IP address 203.0.113.77 for user account casey@cvi-training.example, system audit logs capturing group membership changes (S004 through S009, which record the sequence of failed login attempts, the subsequent unverified sign-in, and the unauthorized self-assignment to the privileged group), and the resulting directory state entries confirming unauthorized access to the Privileged-Operators group.

Evidence IDs (EV-…) and event IDs (S…, A…, C…) refer to records in my Week 11 evidence index; full evidence is not duplicated here.

## 4. Timeline
14:00:00 UTC — S004 — Multiple consecutive failed password attempts for user casey@cvi-training.example originating from remote IP address 203.0.113.77.

14:00:30 UTC — S005 — Continued failed password attempts for the same user account from the same IP address.

14:01:00 UTC — S006 — Further failed authentication attempts recorded during the brute-force sequence.

14:01:30 UTC — S007 — Repeated failed password entry preceding the successful authentication event.

14:02:00 UTC — S008 — Final failed password attempt before the successful login threshold.

14:03:00 UTC — S009 — Successful authentication for casey@cvi-training.example without an MFA challenge, followed immediately by an audit log entry showing the account self-assigning to the Privileged-Operators group with no approval ticket recorded.

## 5. Findings
### Finding 1 (RF1) — confidence: confirmed

The records show that the user account casey@cvi-training.example experienced multiple consecutive failed password attempts originating from an unknown remote device (203.0.113.77) followed by a successful authentication without an MFA challenge, which directly correlated with a subsequent audit log entry showing the account successfully adding itself to the Privileged-Operators group with no approval ticket recorded.

- Evidence / events: S004, S005, S006, S007, S008, S009
- Uncertainty: The records do not show whether the brute-force attempts and subsequent unauthorized group addition were performed by an external malicious actor using those credentials or by an insider operating the device.

### Finding 2 (RF2) — confidence: confirmed

Based on the available records, we can confirm that user blair@cvi-training.example successfully authenticated after an initial password error, and that their subsequent addition to the Junior-Analysts group was properly authorized and logged under change control ticket CHG-1101.
The records show that user blair@cvi-training.example successfully authenticated after an initial password error, and that their subsequent addition to the Junior-Analysts group was properly authorized and logged under change control ticket CHG-1101.

- Evidence / events: S001, S002, S003, S010, S011, A001, A002, A003, A004
- Uncertainty: The records show that user blair@cvi-training.example successfully authenticated following an initial password error, and subsequent audit logs confirm their addition to the Junior-Analysts group under authorized change control ticket CHG-1101.

## 6. Impact / risk
If this activity was not authorised, it could allow an unauthorized actor to retain high-level administrative access via the Privileged-Operators group, impacting the confidentiality and integrity of critical systems by bypassing multi-factor authentication controls.

## 7. Recommendations / next actions
### Recommendation 1 (R1)

- **What:** Within 24 hours, the IT Security team will immediately disable all active credentials and sessions for the affected user account across the directory, completely remove the account from the Privileged-Operators administrative group to eliminate unauthorized elevated access, and enforce mandatory multi-factor authentication requirements with strict verification checks to prevent any future authentication bypass attempts.
- **Who:** IT Security team
- **Why:** This decisive action directly mitigates the severe ongoing risk of sustained unauthorized administrative access, credential misuse, and further lateral movement or privilege escalation within our core environment, thereby protecting critical enterprise systems from malicious exploitation, maintaining strict operational integrity, and restoring compliance with internal access governance standards.
- **Priority:** high
- **Timeframe:** within 24 hours
- **Linked findings:** RF1
- **Success measure:** We will know this recommendation has worked successfully when a comprehensive post-remediation audit confirms that the affected user account status is fully disabled across the directory, the account is completely removed and absent from the Privileged-Operators group membership list, active multi-factor authentication is successfully enforced and verified on the user profile, and subsequent access control logs show zero further unauthorized activity or authentication attempts from that profile.

## 8. Limitations / unknowns
This investigation is limited by the boundaries of a fictional training simulation, missing contextual telemetry regarding off-network user behavior, and the inability to independently verify unconfirmed human factors or external motivations behind routine administrative and user actions.

## 9. Conclusion
Based on the available records, the unauthorized self-assignment of user account casey@cvi-training.example to the Privileged-Operators group following a brute-force attack from IP address 203.0.113.77 confirms a critical credential compromise requiring immediate escalation. Within 0 to 15 minutes of detection, Security Operations Center (SOC) analysts and Identity and Access Management (IAM) administrators must contain the threat by disabling the compromised account, terminating active session tokens, and revoking its membership from the Privileged-Operators group. Within 1 to 2 hours, IAM administrators must enforce a credential reset and verify full log scope, followed by short-term authentication policy hardening by technical leads within 24 hours.

## Appendix — wording I checked against evidence
- "compromised" in Report — Conclusion: Record EV-3 shows that user credentials were used without multi-factor authentication following repeated failed attempts.
- "compromise" in Report — Conclusion: Record EV-4 shows unauthorized modifications made to the Privileged-Operators group membership.
