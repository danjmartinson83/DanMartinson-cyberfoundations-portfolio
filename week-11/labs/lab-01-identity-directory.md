# Lab 01 — Identity Directory: Who Is Who?

**Learner:** Dan Martinson  
**Attempt:** attempt 81B676 · seed chic-w11-v1 · state revision 12 · text revision 23

> Training simulation — fictional Cloud Heights accounts and resources. Your actions change only your Week 11 learning attempt. This is not a live AD domain, Microsoft Entra tenant or Azure subscription.

## Objective

Investigate why one person may have different access in different identity systems.

## My answers

### Difference 1 between the AD and cloud views (what you saw, and why it matters)

Active Directory relies on organizational filing containers (OU-RESP Response) to structure and segment user accounts, whereas Cloud Identity uses flat cloud group structures without organizational unit hierarchies.
This matters because container-based policies and management boundaries in on-premises AD do not automatically transfer or sync to the cloud environment. Security analysts must evaluate permissions and group memberships independently in both directories rather than assuming cloud access mirrors on-prem structure.

### Difference 2 between the AD and cloud views

Active Directory manages access primarily through on-premises security group nesting and physical or organizational placement, whereas Cloud Identity uses explicit cloud roles assigned across cloud resource scopes.
This distinction matters because permissions are enforced by completely different control planes. An identity can appear active or inactive in one domain without immediately altering its authorization state or sign-in capabilities in the other, meaning security teams cannot rely on a single directory audit to understand total organizational access.

### What do Junior-Analysts and Case-Readers actually grant? How did you check?

The GC-JUN (Junior-Analysts) group grants access to operational tasks and queue interaction (such as queue → read and queue → update), whereas the GC-READ (Case-Readers) group grants viewing permissions over investigation case files (such as case read).
I checked this by inspecting the effective access paths and group role assignments in both the Active Directory and Cloud Identity panels, verifying which resource scopes and permissions (RL-RESP and RL-READ) were tied directly to each group membership.

### Why does Drew's person record still exist?

Even though Drew's active directory and cloud accounts are disabled, the core HR/person record is retained for auditing, legal compliance, and historical traceability. Organizations preserve identity records to maintain an accurate audit trail of past access and ownership for investigations or compliance reviews.

## Directory trace

| Concept | Object |
|---|---|
| ou | OU-RESP Response |
| role | RL-RESP Response Agent @ R-QUEUE |
| group | GC-JUN Junior-Analysts |
| person | P01 Alex Morgan |
| account | ad-alex (alex@ad.cloudheights.example) |
| identity | cl-alex.department=DEP-RESP |
| permission | ad_file R-ADRESP → read (ACL) |

## Evidence

- **E01 · EV-81B676-001** — Directory trace: Alex person, both accounts, OU, one AD grant path, one cloud role path (captured at revision 5)  
  _What this proves:_ These snapshots show one person with two accounts. In each directory, I observed that Alex Morgan has separate active records (ad-alex and cl-alex) mapped independently to their respective on-premises Active Directory and Cloud Identity environments.  
  See [evidence index](evidence/week11-evidence-index.md#ev-81b676-001)
- **E02 · EV-81B676-002** — Comparison of Blair, Finley and Drew (captured at revision 12)  
  _What this proves:_ Comparing these accounts, I observed that active cloud accounts (cl-blair and cl-finley) yielded mixed results for the landing resource in access tests, while Drew's disabled accounts (ad-drew and cl-drew) consistently resulted in access denials.  
  See [evidence index](evidence/week11-evidence-index.md#ev-81b676-002)
