# Lab 05 — Joiner, Mover, Leaver

**Learner:** Dan Martinson  
**Attempt:** attempt 81B676 · seed chic-w11-v1 · state revision 193 · text revision 80

> Training simulation — fictional Cloud Heights accounts and resources. Your actions change only your Week 11 learning attempt. This is not a live AD domain, Microsoft Entra tenant or Azure subscription.

## Objective

Complete four lifecycle tickets across the two directory surfaces, plus a short Azure scope comparison.

## My answers

### T501 decision table — Add / Retain / Remove / Deny / Escalate (write 'not applicable — reason' where needed)

Add: Junior-Analysts (GC-JUN) and Case-Readers (GC-READ) group memberships for cl-jamie.
Retain: Existing Active Directory account (ad-jamie).
Remove: Not applicable — no pre-existing conflicting cloud memberships or roles required removal for a new cloud onboarding.
Deny: Not applicable — all requested and verified joiner actions were approved.
Escalate: Not applicable — identity verification passed successfully via directory-confirmed callback and HR ID (CH-008).

### T502 decision table — Add / Retain / Remove / Deny / Escalate

Add: Audit-Team (GA-AUD) and Audit-Reviewers (GC-AUD) group memberships for Alex Morgan across Active Directory and Cloud Identity, plus staff handbook access preservation.
Retain: Existing staff handbook access and user accounts (ad-alex, cl-alex).
Remove: Old operational memberships (Response-Team / GA-RESP and Response-Operators / GC-RESP) across both directories.
Deny: Not applicable — all approved transfer operations and access adjustments succeeded successfully.
Escalate: Not applicable — HR transfer notice (HR-502) and Audit lead approval (APP-502) fully authorized the move from Response to Audit.

### T503 decision table — Add / Retain / Remove / Deny / Escalate

Add: Not applicable — offboarding ticket T503 required revocation and removal of access, not the addition of new privileges. Retain: Audit logs and records of Finley's previous access and offboarding actions as required by the termination ticket. Remove: Active memberships in both directories (Active Directory and Cloud Identity), active user sessions, and moved the Active Directory account to the Disabled Accounts organizational unit (OU). Deny: Old-session access retest (Case Summaries / read) and new sign-in attempts (ACCOUNT_DISABLED). Escalate: Not applicable — HR termination approval (HR-503) was fully authorized and complete, requiring immediate offboarding without exception.

### T504 decision table — Add / Retain / Remove / Deny / Escalate

Add: Not applicable — ticket T504 requested a password reset, which was unverified and denied, so no permissions or memberships were added.
Retain: Existing user account status and credentials for cl-blair until proper verification can be established.
Remove: Not applicable — no access changes or removals were required for an unauthenticated request.
Deny: Password reset request for cl-blair, as the caller-supplied employee ID (CH-099) and callback route failed verification against Blair Chen's official HR record (CH-002).
Escalate: Ticket T504 was set to escalated after identity verification failed to prevent unauthorized credential modification.

### Why is an Azure resource role/scope different from a cloud directory role?

An Azure resource role and scope differs from a cloud directory role in scope, target, and function:

Azure Resource Role & Scope: Operates on Azure cloud infrastructure (such as virtual machines, storage accounts, or resource groups like RG-LAB). It authorizes specific operations on specific resources (e.g., reading metadata or stopping a VM) using Azure Role-Based Access Control (RBAC) without granting any authority over user accounts or tenant-wide directory settings.

Cloud Directory Role: Operates at the tenant level across identity management services (such as Microsoft Entra ID / Cloud Identity). It governs user provisioning, group memberships, credential resets, and administrative access across directory objects, rather than individual cloud infrastructure resources.

## Evidence

- **E12 · EV-81B676-017** — Jamie joiner chain (captured at revision 137)  
  _What this proves:_ Jamie’s joiner records show that cloud identity account cl-jamie was successfully created, verified, MFA-enrolled, enabled, and assigned to the Junior-Analysts and Case-Readers groups under ticket T501. The access tests record that the account is permitted to read case summaries but denied updates due to lacking appropriate permissions.  
  See [evidence index](evidence/week11-evidence-index.md#ev-81b676-017)
- **E13 · EV-81B676-018** — Alex before/after access and changes (captured at revision 142)  
  _What this proves:_ At this point in Alex’s move, the account snapshots and tests show Alex’s active accounts (ad-alex and cl-alex) in their initial Response department configuration with corresponding allowed/denied baseline access tests. The changes recorded are none yet, establishing the baseline prior to executing ticket T502.  
  See [evidence index](evidence/week11-evidence-index.md#ev-81b676-018)
- **E13 · EV-81B676-019** — Alex before/after access and changes (captured at revision 155)  
  _What this proves:_ At this point in Alex’s move, the account snapshots and tests show Alex’s accounts updated to the Audit department with successful access to audit resources and denied access to old response resources. The changes recorded are the successful transfer of department, removal of old operational group memberships, and addition of new audit memberships across both Active Directory and Cloud Identity under ticket T502.  
  See [evidence index](evidence/week11-evidence-index.md#ev-81b676-019)
- **E14 · EV-81B676-020** — Finley session/status/revocation evidence (captured at revision 182)  
  _What this proves:_ After the leaver actions, the old-session test shows DENY for Case Summaries / read and the new sign-in records show failure due to the account being disabled.  
  See [evidence index](evidence/week11-evidence-index.md#ev-81b676-020)
- **E15 · EV-81B676-021** — Failed reset verification, refusal and escalation (captured at revision 185)  
  _What this proves:_ The verification record shows that identity verification for Blair's reset request was refused due to mismatched details. The ticket-status audit records show that ticket T504 was subsequently escalated.  
  See [evidence index](evidence/week11-evidence-index.md#ev-81b676-021)
- **E16 · EV-81B676-022** — AD DS – Entra – Azure comparison and scoped tests (captured at revision 191)  
  _What this proves:_ The assignment audit records scope Blair's permissions to the Training-VM resource group via the assigned Azure reader role. The three resource tests show that Blair is allowed to read Training-VM metadata, but is denied from stopping the Training-VM and from accessing other teams' virtual machines.  
  See [evidence index](evidence/week11-evidence-index.md#ev-81b676-022)
- **E13 · EV-81B676-023** — Alex before/after access and changes (captured at revision 192)  
  _What this proves:_ At this point in Alex’s move, the account snapshots and tests show Alex's initial enabled status and baseline access permissions across Active Directory and Cloud Identity prior to any department transfer changes. The changes recorded are baseline access evaluations before executing ticket T502.  
  See [evidence index](evidence/week11-evidence-index.md#ev-81b676-023)
- **E12 · EV-81B676-024** — Jamie joiner chain (captured at revision 192)  
  _What this proves:_ Jamie’s joiner records show the successful creation of the Cloud Identity account, identity verification, MFA enrollment, status enablement, credential change, and group membership assignment. The access tests record Jamie's authorized ability to read case summaries and the appropriate denial for case updates.  
  See [evidence index](evidence/week11-evidence-index.md#ev-81b676-024)
