# Executive Summary — Cloud Heights Identity Investigation

> Fictional training scenario: Cloud Heights Identity Center (simulated). No real organisation, people or systems.

- Prepared by: Dan Martinson
- Audience: Cloud Heights leadership
- Length: 265 words (target about 250–400)
- Full technical detail: [technical-incident-report.md](technical-incident-report.md)

## What happened?
During our comprehensive security review and routine log analysis, our incident response team discovered that an unauthorized external party successfully guessed a user account password through a sustained series of repeated login attempts originating from an external IP address. Once inside the enterprise system, this unauthorized actor surreptitiously and illegally granted themselves elevated administrative permissions and high-level system access rights without ever submitting formal approval tickets or following standard change management procedures, thereby completely bypassing all internal controls and security protocols.

## Why does it matter?
An unauthorized user with elevated administrative privileges poses a severe, immediate risk to our data integrity, core system security, and ongoing regulatory compliance. Without proper change controls or formal approvals, leadership lacks critical oversight on what changes were actually made, potentially exposing sensitive business operations or leaving our systems vulnerable to further exploitation and data loss.

## What did we find?
Our forensic investigation confirmed that a specific user account was accessed through repeated login attempts from an unknown remote location, followed by a successful sign-in that bypassed the multi-factor authentication check. Immediately afterward, this account granted itself high-level administrative permissions without any required management approval or tracking tickets.

## What should happen next?
To prevent further risk and secure our infrastructure, we must immediately disable the affected user credentials, revoke the unauthorized administrative permissions, enforce mandatory multi-factor authentication across all user accounts, and conduct a thorough security audit of our access control logs to ensure no other accounts were affected during the incident.

## What remains uncertain
The available records do not definitively establish whether the unauthorized access attempts and subsequent group modification were executed by an external actor using those credentials or by an internal user.
