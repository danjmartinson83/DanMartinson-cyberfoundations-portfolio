# Week 11 evidence index

Simulator captures from attempt 81B676. Hash detects content changes; it is not proof of live AD administration.

## EV-81B676-001

- Slot E01 · M01 · revision 5
- Directory trace: Alex person, both accounts, OU, one AD grant path, one cloud role path
- SHA-256 045d27ffbb77bce6b02dc6a51c62e2b01c1a699eace8ee8c17057b3aa6c28ef3
- Caption: These snapshots show one person with two accounts. In each directory, I observed that Alex Morgan has separate active records (ad-alex and cl-alex) mapped independently to their respective on-premises Active Directory and Cloud Identity environments.

## EV-81B676-002

- Slot E02 · M01 · revision 12
- Comparison of Blair, Finley and Drew
- SHA-256 5062c474234d8cc1ce19552c0d5935239807e3cf88f6df4267240003961269a3
- Caption: Comparing these accounts, I observed that active cloud accounts (cl-blair and cl-finley) yielded mixed results for the landing resource in access tests, while Drew's disabled accounts (ad-drew and cl-drew) consistently resulted in access denials.

## EV-81B676-003

- Slot E01 · M01 · revision 23
- Directory trace: Alex person, both accounts, OU, one AD grant path, one cloud role path
- SHA-256 d79a22567f6a3e1228dcad7ca78a81565d7ace9ae6538f7f89d8f1de04826d5d
- Caption: These snapshots show one person with two accounts. In each directory, I observed that Alex Morgan has independent records (ad-alex and cl-alex) mapped separately to the Active Directory and Cloud Identity environments.

## EV-81B676-004

- Slot E02 · M01 · revision 23
- Comparison of Blair, Finley and Drew
- SHA-256 ef5709d20412b51299317a61e8928b9f0d51305240fedc11d1c10ff593ebaeeb
- Caption: Comparing these accounts, I observed that active cloud accounts (cl-blair and cl-finley) maintained successful sign-ins and varied access results, whereas Drew's disabled accounts (ad-drew and cl-drew) consistently resulted in explicit access denials.

## EV-81B676-005

- Slot E03 · M02 · revision 25
- Successful sign-in + the access result before your change
- SHA-256 c29a81a4baa2f86219f54aadc7e25da24ac35ae263357200d1e52779b23c93a2
- Caption: The sign-in record shows that Blair successfully authenticated. The before-change access test records show the access decision for the requested resource before any changes were made.

## EV-81B676-006

- Slot E04 · M02 · revision 36
- Membership/access change audit + read result + update result
- SHA-256 b63e8e2b6ad46ec00552c227cc5f93cdc5fbce4352d0a91c49e6af5d4a67987c
- Caption: The audit records the change to add Blair to the Case-Readers group. The retests show that Blair is now allowed to read Case Summaries while update access remains denied.

## EV-81B676-007

- Slot E03 · M02 · revision 37
- Successful sign-in + the access result before your change
- SHA-256 ca35c5c23f075b56efb3640a6e4c723b2172154cae87f0ea567dae740eb54394
- Caption: The sign-in record shows that Blair successfully authenticated. The before-change access test records show a DENY decision for the requested Case Summaries read access before any configuration changes were made.

## EV-81B676-008

- Slot E06 · M03 · revision 50
- Passed verification + reset version change
- SHA-256 fa88605525cb9c60e0c94becf728f6e5d402c65083b46ade066b50947d18202a
- Caption: The verification audit shows identity verification was successfully completed for T302. The reset audit records the password reset execution for ad-jamie under T302.

## EV-81B676-009

- Slot E07 · M03 · revision 62
- Disable / re-enable / session validation sequence
- SHA-256 7226af34b260e522a1ab3c905413a39ab2044d125ce6ad1b6cae2bdb6f29a619
- Caption: In sequence, the status changes and tests show that when Jamie's account was disabled, access tests resulted in DENY and sign-ins failed due to the disabled state, and upon re-enabling, access tests returned ALLOW and sign-ins succeeded.

## EV-81B676-010

- Slot E05 · M03 · revision 62
- Created account with OU and groups
- SHA-256 8415cd2c92f3e08038d009035b33b3aece7982c7c2ecb3980e0ef0a728802238
- Caption: Jamie’s account snapshot shows the OU placement and groups assigned to ad-jamie within Active Directory.

## EV-81B676-011

- Slot E05 · M03 · revision 62
- Created account with OU and groups
- SHA-256 8415cd2c92f3e08038d009035b33b3aece7982c7c2ecb3980e0ef0a728802238
- Caption: Jamie’s account snapshot shows the OU placement for ad-jamie and the assigned groups granting the correct access level.

## EV-81B676-012

- Slot E08 · M04 · revision 101
- Three job configuration snapshots with rationales
- SHA-256 d0277ed4d8f63e731b9d7355f99fbb293bb17f445a11cf8b834ef7bc0ed5f0a3
- Caption: These configurations show the updated cloud group memberships for Blair, Casey, and Emi. My review records explain the rationale and least-privilege role assignments applied for each user.

## EV-81B676-013

- Slot E09 · M04 · revision 113
- The nine required access tests
- SHA-256 86a0aa23fffbf71bb7be38cd2f74a65f56ba4c840dcca9134c138959dbc3cbed
- Caption: These tests record each account’s requested actions and decisions: verifying whether Blair, Casey, and Emi are granted or denied specific read, update, export, and delete actions against the target resources under their current access levels.

## EV-81B676-014

- Slot E10 · M04 · revision 117
- Temporary grant → allowed test → revoke → denied retest
- SHA-256 3d0a018fa70b951b581a91292db18d9cd7ad45a61d56bcaf22d6e5b6c2b7d0b9
- Caption: Before and after removing the temporary membership, the tests show that Blair's access to read audit evidence changed from allowed while in the review group to denied once the membership was revoked.

## EV-81B676-015

- Slot E11 · M04 · revision 122
- Four ABAC cases (current + three what-ifs)
- SHA-256 f9ecb9de67ff17642c9ad71a2f1faadd7441219dc688efb834537b2da1b8976d
- Caption: The current state test shows allowed access for Casey to read internal response notes under valid attributes. Changing one attribute at a time produced denied access results when device trust, department, or classification constraints failed.

## EV-81B676-016

- Slot E08 · M04 · revision 125
- Three job configuration snapshots with rationales
- SHA-256 67bf5a899974068b1ad1b329fdb07a26de424b4cd276b27a6fc35332a9ad9cae
- Caption: These configurations show the updated cloud account memberships and least privilege group assignments for Blair, Casey, and Emi. My review records explain the specific group additions, removals, and ticket resolutions taken to enforce authorized access boundaries.

## EV-81B676-017

- Slot E12 · M05 · revision 137
- Jamie joiner chain
- SHA-256 1162a1cf9eb056bf4a7d04849039797c80ac74db416327d8a51457ebce3d0a52
- Caption: Jamie’s joiner records show that cloud identity account cl-jamie was successfully created, verified, MFA-enrolled, enabled, and assigned to the Junior-Analysts and Case-Readers groups under ticket T501. The access tests record that the account is permitted to read case summaries but denied updates due to lacking appropriate permissions.

## EV-81B676-018

- Slot E13 · M05 · revision 142
- Alex before/after access and changes
- SHA-256 9f80e6ca8996fd0ca48557d0b6dff01cf1a2560fef505e5d9119d6f9c6dcb809
- Caption: At this point in Alex’s move, the account snapshots and tests show Alex’s active accounts (ad-alex and cl-alex) in their initial Response department configuration with corresponding allowed/denied baseline access tests. The changes recorded are none yet, establishing the baseline prior to executing ticket T502.

## EV-81B676-019

- Slot E13 · M05 · revision 155
- Alex before/after access and changes
- SHA-256 561c5a580c1c04b20aac69d6603584006f7667eaa0699959b341a8568ddfa5d0
- Caption: At this point in Alex’s move, the account snapshots and tests show Alex’s accounts updated to the Audit department with successful access to audit resources and denied access to old response resources. The changes recorded are the successful transfer of department, removal of old operational group memberships, and addition of new audit memberships across both Active Directory and Cloud Identity under ticket T502.

## EV-81B676-020

- Slot E14 · M05 · revision 182
- Finley session/status/revocation evidence
- SHA-256 0e8622909132634084db9e3dcd0086b573ea0565ccd30ba3297ad5fefaaf6709
- Caption: After the leaver actions, the old-session test shows DENY for Case Summaries / read and the new sign-in records show failure due to the account being disabled.

## EV-81B676-021

- Slot E15 · M05 · revision 185
- Failed reset verification, refusal and escalation
- SHA-256 d2464dff65df80ad1a3e39e14fd59f49462a2b5fed96d5a9fea7a8ffd20c8f39
- Caption: The verification record shows that identity verification for Blair's reset request was refused due to mismatched details. The ticket-status audit records show that ticket T504 was subsequently escalated.

## EV-81B676-022

- Slot E16 · M05 · revision 191
- AD DS – Entra – Azure comparison and scoped tests
- SHA-256 b54eb29b952e66cbaea597a22e82548506d1ade23ebc9ead5474184ecdb19928
- Caption: The assignment audit records scope Blair's permissions to the Training-VM resource group via the assigned Azure reader role. The three resource tests show that Blair is allowed to read Training-VM metadata, but is denied from stopping the Training-VM and from accessing other teams' virtual machines.

## EV-81B676-023

- Slot E13 · M05 · revision 192
- Alex before/after access and changes
- SHA-256 94568e2bec52591bdff72bb277e937ef95067e393cbf87881cc7fe36e80c89c2
- Caption: At this point in Alex’s move, the account snapshots and tests show Alex's initial enabled status and baseline access permissions across Active Directory and Cloud Identity prior to any department transfer changes. The changes recorded are baseline access evaluations before executing ticket T502.

## EV-81B676-024

- Slot E12 · M05 · revision 192
- Jamie joiner chain
- SHA-256 14f4fad6fe5e9210b3303c280f20f25b7453eb1cdbaffd90844de32e4bfca1d2
- Caption: Jamie’s joiner records show the successful creation of the Cloud Identity account, identity verification, MFA enrollment, status enablement, credential change, and group membership assignment. The access tests record Jamie's authorized ability to read case summaries and the appropriate denial for case updates.

## EV-81B676-025

- Slot E17 · M06 · revision 193
- Two distinct findings with raw-event references and correlation
- SHA-256 e8f89c8f79f1eaa4674345645ef4ec8bca0816fffabcf996a6acecff53f76a4f
- Caption: These records support my observation that historical sign-in and audit events exhibit correlated administrative actions and session continuations across distinct timestamps. Their correlation shows temporal relationships between authentication attempts and group modifications, but does not establish the underlying intent or external human factors behind those events.

## EV-81B676-026

- Slot E18 · M06 · revision 193
- Benign/ambiguous comparison
- SHA-256 42ce353a65fd10205425d54ba2a119c2fa4d4dbca9a2de017b04f304bf2b2b78
- Caption: These records show an initial authentication failure due to an incorrect password followed immediately by a successful sign-in attempt. The information is limited because it captures only authentication outcomes without providing context on whether the initial failure was a simple typographical error or indicative of suspicious activity.

## EV-81B676-027

- Slot E17 · M06 · revision 202
- Two distinct findings with raw-event references and correlation
- SHA-256 a7a03696284c506a5b8a92b3c5c9bc05d02d2c7859b3510f5cd7d5c032b5b803
- Caption: These records support my observation that multiple failed authentication attempts preceded a successful sign-in on the target account. Their correlation shows event sequencing and administrative changes, but does not establish user intent.

## EV-81B676-028

- Slot E19 · M06 · revision 202
- Completed case file / versioned export
- SHA-256 a7a03696284c506a5b8a92b3c5c9bc05d02d2c7859b3510f5cd7d5c032b5b803
- Caption: My downloaded Case File references these records to support the analysis of authentication anomalies and administrative group modifications.
