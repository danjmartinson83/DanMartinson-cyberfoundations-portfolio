# Lab 04 — Least Privilege Challenge

**Learner:** Dan Martinson  
**Attempt:** attempt 81B676 · seed chic-w11-v1 · state revision 125 · text revision 67

> Training simulation — fictional Cloud Heights accounts and resources. Your actions change only your Week 11 learning attempt. This is not a live AD domain, Microsoft Entra tenant or Azure subscription.

## Objective

Configure three job-role assignments, remove excess access, and test role-based and attribute-based access.

## My answers

### Blair, Casey, Emi: job, required actions, forbidden actions

Blair
Junior Analyst responsible for reviewing assigned case summaries and participating in initial triage.
Required actions: Read and update assigned case summaries.
Forbidden actions: Directory administration, modifying audit evidence, or accessing response queues.

Casey
Response Operator responsible for managing active security incidents and response queues.
Required actions: Read and update response queues, and read the Internal Response Note.
Forbidden actions: Deleting audit evidence or performing directory administration.

Emi
Audit Reviewer responsible for compliance checks and reviewing audit evidence. Required actions: Read and export audit evidence. 
Forbidden actions: Deleting audit evidence or modifying operational response queues.

### Prediction for the three what-if cases, then which attribute changed each result

For the device trust what-if case, changing the device state from managed to unmanaged will result in a DENY because conditional access policies require a trusted device context. For the department what-if case, changing the department attribute will result in a DENY since the user no longer matches the resource's required department scope. For the classification what-if case, changing the resource classification to confidential will result in a DENY because the role lacks clearance for higher-sensitivity data.

### RBAC and assignment scope in your own words

Role-based access control (RBAC) groups permissions into specific roles so users are granted access based on their job functions rather than individual permissions. Assignment scope further restricts those roles by defining precisely where and on what resources those permissions apply (such as a specific management group or resource group)

### Least privilege — what you removed and why

To comply to the principle of least privilege, excess memberships and overly broad permissions were removed from the analyst accounts. Specifically, extraneous group assignments that granted unnecessary access beyond each role's specific operational requirements—such as unneeded audit and administrative queue privileges—were revoked to ensure users only possess the minimum permissions necessary for their assigned job duties.

### Why sign-in didn't settle authorization, and how ABAC adds conditions

Sign-in only handles authentication by verifying who the user is, whereas authorization determines what resources they are allowed to access based on their roles and permissions. Attribute-based access control (ABAC) further refines authorization by dynamically evaluating environmental and contextual conditions—such as device trust state, department, and resource classification—at the exact moment access is requested.

## Evidence

- **E08 · EV-81B676-012** — Three job configuration snapshots with rationales (captured at revision 101)  
  _What this proves:_ These configurations show the updated cloud group memberships for Blair, Casey, and Emi. My review records explain the rationale and least-privilege role assignments applied for each user.  
  See [evidence index](evidence/week11-evidence-index.md#ev-81b676-012)
- **E09 · EV-81B676-013** — The nine required access tests (captured at revision 113)  
  _What this proves:_ These tests record each account’s requested actions and decisions: verifying whether Blair, Casey, and Emi are granted or denied specific read, update, export, and delete actions against the target resources under their current access levels.  
  See [evidence index](evidence/week11-evidence-index.md#ev-81b676-013)
- **E10 · EV-81B676-014** — Temporary grant → allowed test → revoke → denied retest (captured at revision 117)  
  _What this proves:_ Before and after removing the temporary membership, the tests show that Blair's access to read audit evidence changed from allowed while in the review group to denied once the membership was revoked.  
  See [evidence index](evidence/week11-evidence-index.md#ev-81b676-014)
- **E11 · EV-81B676-015** — Four ABAC cases (current + three what-ifs) (captured at revision 122)  
  _What this proves:_ The current state test shows allowed access for Casey to read internal response notes under valid attributes. Changing one attribute at a time produced denied access results when device trust, department, or classification constraints failed.  
  See [evidence index](evidence/week11-evidence-index.md#ev-81b676-015)
- **E08 · EV-81B676-016** — Three job configuration snapshots with rationales (captured at revision 125)  
  _What this proves:_ These configurations show the updated cloud account memberships and least privilege group assignments for Blair, Casey, and Emi. My review records explain the specific group additions, removals, and ticket resolutions taken to enforce authorized access boundaries.  
  See [evidence index](evidence/week11-evidence-index.md#ev-81b676-016)
