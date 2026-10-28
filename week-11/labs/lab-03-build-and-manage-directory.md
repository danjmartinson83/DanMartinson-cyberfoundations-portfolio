# Lab 03 — Build and Manage the Directory

**Learner:** Dan Martinson  
**Attempt:** attempt 81B676 · seed chic-w11-v1 · state revision 88 · text revision 41

> Training simulation — fictional Cloud Heights accounts and resources. Your actions change only your Week 11 learning attempt. This is not a live AD domain, Microsoft Entra tenant or Azure subscription.

## Objective

Create Jamie's AD account, place it, grant basic group access, and verify, reset and enable it safely.

## My answers

### What did OU placement change — and not change?

OU placement changed the account's location within the Active Directory directory tree structure, placing it in the correct organizational unit according to ticket requirements. It did not automatically grant specific permissions or change group memberships by itself.

### What did group membership change?

Group membership changed the account's authorization scope by adding ad-jamie to the necessary security groups, granting the account the baseline permissions associated with those groups.

### What did the credential reset change? Why did verification come first?

The credential reset changed the account's password version and established initial secure sign-in credentials. Verification came first to ensure the identity of the user requesting the change was properly authenticated via authorized callback evidence before performing a sensitive administrative action.

### What did disabling and re-enabling do to sessions and access?

Disabling the account immediately terminated active sessions and resulted in access test denials (DENY), while re-enabling the account restored session capability and allowed access tests to return ALLOW as verified during the validation sequence.

## Evidence

- **E06 · EV-81B676-008** — Passed verification + reset version change (captured at revision 50)  
  _What this proves:_ The verification audit shows identity verification was successfully completed for T302. The reset audit records the password reset execution for ad-jamie under T302.  
  See [evidence index](evidence/week11-evidence-index.md#ev-81b676-008)
- **E07 · EV-81B676-009** — Disable / re-enable / session validation sequence (captured at revision 62)  
  _What this proves:_ In sequence, the status changes and tests show that when Jamie's account was disabled, access tests resulted in DENY and sign-ins failed due to the disabled state, and upon re-enabling, access tests returned ALLOW and sign-ins succeeded.  
  See [evidence index](evidence/week11-evidence-index.md#ev-81b676-009)
- **E05 · EV-81B676-010** — Created account with OU and groups (captured at revision 62)  
  _What this proves:_ Jamie’s account snapshot shows the OU placement and groups assigned to ad-jamie within Active Directory.  
  See [evidence index](evidence/week11-evidence-index.md#ev-81b676-010)
- **E05 · EV-81B676-011** — Created account with OU and groups (captured at revision 62)  
  _What this proves:_ Jamie’s account snapshot shows the OU placement for ad-jamie and the assigned groups granting the correct access level.  
  See [evidence index](evidence/week11-evidence-index.md#ev-81b676-011)
