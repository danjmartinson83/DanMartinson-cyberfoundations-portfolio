# Week 10 Notes — Security Fundamentals and Risk

**Student Name:** Dan Martinson

**Date:** 10/17/2026

Use your own words and everyday examples. These notes support your thinking; they are not your lab answers. Do not copy clinic scenario answers here — those belong in the Demo Lab.

## 1. Assets and Business Purpose

An asset is something a business depends on. Pick an everyday example (a bakery, a gym, a school).

```text
My everyday business: A local 24-hour neighborhood fitness center ("Iron & Health Gym").
One asset it depends on: The digital member database and keycard access control system.
Why the business needs that asset: To securely manage active member subscriptions, track who enters the facility, and allow automated 24/7 door access.
```

## 2. Confidentiality, Integrity, Availability

Define each goal in your own words, then describe one situation where more than one goal is affected and explain why.

```text
Confidentiality means: Keeping private information restricted to authorized eyes only (e.g., protecting members' home addresses, phone numbers, and payment details).
Integrity means: Ensuring data remains accurate and unaltered by unauthorized parties (e.g., ensuring a member's active payment status isn't accidentally or maliciously flipped to "expired").
Availability means: Ensuring systems and facilities can be accessed and used when needed (e.g., the keycard entry scanners work reliably so members can get inside for their workouts).
A situation where goals overlap, and why: An intruder compromises the administrative database, altering digital waivers and membership statuses (violating integrity), which causes the automated entry system to lock everyone out and halt gym operations completely (violating availability).
```

## 3. Event, Weakness, Consequence and Risk

Use your OWN non-clinic example to separate these four ideas.

```text
My example setting: The gym's front desk computer, which stays logged into the membership management software all day.
Threat / event (what could happen): An unauthorized visitor walks behind the front desk while staff are busy helping someone else and accesses member files on the screen.
Vulnerability (the weakness that lets it cause harm): The front desk computer lacks an automatic screen-timeout lock and has no physical barrier blocking public access to the desk area.
Consequence (what goes wrong if it happens): Sensitive personal information belonging to hundreds of members is exposed or copied.
Risk (how the pieces combine into something to manage): The likelihood of a casual visitor exploiting an unattended, unlocked front desk screen, leading to potential personal data leakage.
```

## 4. Observed, Inferred and Unknown

Evidence you saw is different from a guess. If you did not see a safeguard, it is unknown — not proof it is missing.

```text
Something I observed directly: The emergency back door of the gym was propped open with a rubber wedge during midday hours.
Something I inferred from it: Staff members were likely moving equipment or letting fresh air in and forgot to remove the wedge.
Something that is still unknown: Whether anyone unauthorized slipped through the propped door while nobody was looking.
How I will label a safeguard I did not see: "Unverified / Not Observed" (not jumping to conclusions that an alarm system is completely broken just because I didn't see it test-fired).
```

## 5. Warning Signs and Safe Reporting

Suspicious is not the same as proven.

```text
Warning signs I would look for: Receiving an unexpected email from the gym's billing processor asking for staff admin credentials to "verify account compliance."
How I would safely verify without clicking or replying: Check with the general manager or look up the processor's official contact information independently to ask if they sent the request.
Who I would report to, and how: Report it to the gym owner or operations manager via the official staff messaging channel.
Why suspicion alone does not prove compromise: A phishing email arriving in an inbox proves someone tried to scam us, but it doesn't mean anyone actually clicked the link or compromised the system.
```

## 6. Likelihood and Impact

Likelihood and impact are each rated 1–3. The classroom score is Likelihood x Impact. Bands: 1–2 low, 3–4 medium, 6–9 high. These are classroom judgments, not measured probabilities.

```text
What a likelihood of 1, 2 or 3 means to me: 1 = Unlikely (rarely or never occurs)

2 = Possible (could happen if conditions line up)

3 = Probable (frequently attempted or expected based on trends)
What an impact of 1, 2 or 3 means to me: 1 = Minor inconvenience (small delay, easily fixed)

2 = Moderate disruption (affects daily workflow or temporary member annoyance)

3 = Severe disruption (halts business operations entirely or causes massive legal/financial loss)
Existing controls vs proposed controls, in my words: Existing controls are the safeguards already protecting us today (like physical keycards), while proposed controls are the new measures we want to add (like multi-factor authentication for admin logins).
Why recording my reason matters more than the number: The number is just a quick score, but the written explanation provides the crucial context of why we chose that rating so anyone reading it understands our reasoning.
```

## 7. Controls and Residual Risk

Use a non-clinic example.

```text
A specific control: Setting up automatic screen-timeout locks on all employee computers after 5 minutes of inactivity.
How it helps: Prevents walk-in visitors or unauthorized people from snooping at unattended front desk dashboards.
Risk remaining afterwards: A staff member could still write their password on a sticky note and stick it to the monitor, leaving a physical security loophole that software locks can't fix.
```

## 8. Talking to a Manager

```text
How I would explain a risk in plain language to a non-technical manager: Right now, anyone walking up to the front desk can see open member records on our unlocked computer screen if staff step away. We should set up automatic screen locks so our customer data stays private when the desk is unattended.
```

## 9. Questions and Terms to Revisit

```text
Terms I want to review: Residual risk, administrative controls vs. technical controls.
Questions for my instructor: How do we properly document a risk when a control exists on paper, but staff frequently bypass it?
```
