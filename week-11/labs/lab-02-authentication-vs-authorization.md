# Lab 02 — Authentication vs. Authorization: A Valid Badge Doesn't Open Every Door

**Learner:** Dan Martinson  
**Attempt:** attempt 81B676 · seed chic-w11-v1 · state revision 37 · text revision 33

> Training simulation — fictional Cloud Heights accounts and resources. Your actions change only your Week 11 learning attempt. This is not a live AD domain, Microsoft Entra tenant or Azure subscription.

## Objective

Diagnose and repair Blair's missing case access without granting update rights.

## My answers

### Prediction before testing: will Blair be able to read cases? Why?

Blair will not be able to read case summaries initially. While her account can successfully authenticate (sign in), she lacks the necessary authorization—such as membership in the appropriate case-reader group—to access the resource.

### Identification — using the actual account

Identification uses the actual account (cl-blair) to establish who is attempting access. The system recognizes the user based on this unique account identifier before checking credentials or permissions.

### Authentication — using your sign-in event

Authentication verifies the user's identity using the successful sign-in event for cl-blair. This confirms that the credentials and multi-factor authentication provided matched the expected identity before any authorization decisions were made.

### Authorization — using your access tests

Authorization uses the access test records to verify whether Blair's assigned roles and group memberships grant her permission to access the Case Summaries resource, demonstrating the distinction between holding a valid identity and being permitted to perform specific actions.

### Accountability — using the audit record

Accountability uses the audit records to track configuration changes and access attempts back to the administrator who performed them, ensuring traceability and responsibility for all modifications made during the investigation.

## Evidence

- **E03 · EV-81B676-005** — Successful sign-in + the access result before your change (captured at revision 25)  
  _What this proves:_ The sign-in record shows that Blair successfully authenticated. The before-change access test records show the access decision for the requested resource before any changes were made.  
  See [evidence index](evidence/week11-evidence-index.md#ev-81b676-005)
- **E04 · EV-81B676-006** — Membership/access change audit + read result + update result (captured at revision 36)  
  _What this proves:_ The audit records the change to add Blair to the Case-Readers group. The retests show that Blair is now allowed to read Case Summaries while update access remains denied.  
  See [evidence index](evidence/week11-evidence-index.md#ev-81b676-006)
- **E03 · EV-81B676-007** — Successful sign-in + the access result before your change (captured at revision 37)  
  _What this proves:_ The sign-in record shows that Blair successfully authenticated. The before-change access test records show a DENY decision for the requested Case Summaries read access before any configuration changes were made.  
  See [evidence index](evidence/week11-evidence-index.md#ev-81b676-007)
