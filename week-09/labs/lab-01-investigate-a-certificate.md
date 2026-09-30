# Week 9 Lab 01 - Investigate a Certificate

**Student Name:** Dan Martinson

**Date Completed:** 9/28/2026

**Module:** 3 - Practical Cryptography | **Week:** 9  
**Submission Path:** `week-09/labs/lab-01-investigate-a-certificate.md`

> ## Vault Exchange Trust and Key Safety Rule
> Inspect a public website without signing in. Do not click past a browser certificate warning, add a practice issuing office (CA) to your browser’s accepted list, or upload secret private keys. Keep all Week 6-8 VM files, SSH keys, and access settings unchanged. This lab makes no security-rule changes.
>
> **Evidence safety:** Capture the certificate viewer, not your account, bookmarks, browser address bar, passwords, or Bastion access URL. Record the public hostname as text in this worksheet.

---

## Mission

Ivy has two digital keys. Both say “Vault Exchange Support.” How can she tell which one belongs to the support team? A label alone is not enough.

Think of a visitor showing a badge at a front desk. The guard checks the name, the dates, and the office that issued it. In this lab, you will look at a website’s digital badge, called a **certificate**. You will write down what you see and follow the list of offices that signed it. You are looking and recording; you are not changing the website.

A visitor badge has a name, issuing office, validity period, and permitted use. A certificate similarly supplies information to check. A polished badge does not make its issuer trusted, and a certificate does not guarantee that a website's advice or downloads are safe.

## What You Already Know

You do not need to memorize last week’s vocabulary. Use these reminders:

- A **public key** is the shareable part of a pair of digital keys. Its label alone does not prove who owns it.
- A **private key** is the secret part. Keep it private, like a key to a locked room.
- A **digital signature** is a mathematical check made with a private key. It helps detect changes and check which matching key signed something.
- A **browser** is the app you use to visit websites. It checks certificates for you.
- A **hostname** is a website’s name, such as `example.com`. It does not include `https://` or the page name after the slash.

Our question is: “Does this digital badge fit the website I meant to visit, and does my browser accept the office behind it?”

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Environment | Your normal desktop browser; assigned VM is not needed for this investigation |
| Public target | Start with `https://example.com`; use an instructor-approved public HTTPS site if unavailable |
| Change level | Read-only inspection; no sign-in, certificate import, or warning bypass |
| Time | 35-50 minutes; pause and resume as needed |
| Evidence | Certificate fields, browser chain view, dated observations, and your explanation |

- [x] I have watched Lessons 1-3 or reviewed their slides.

- [x] I can open the public site without signing in.

- [x] I know that live issuer names and dates may differ from the lesson images.

- [x] I will write “not observed” when the viewer does not expose a field.

### Cloud Heights Idle Stop

This browser investigation can be completed while your VM is stopped. If you also open Cloud Heights, respond to its idle warning only while actively working. Restart a stopped VM from My Lab Environment when you need it; do not rebuild it.

## Predict First

A visitor’s badge has not expired. Is checking the date enough to let that visitor in? What else should the guard check? Connect your prediction to a website’s certificate in 2–3 sentences. A prediction is your best guess before investigating; it does not have to be correct.

```text
Checking the expiration date alone is not enough to let a visitor in. As a guard, I must also check the visitor’s identity (their name), verify if they are authorized to enter the specific destination, and ensure the badge was issued by a trusted authority rather than forged. Similarly, for a website’s certificate, my browser must verify that the target domain matches the hostname listed on the certificate and that it was signed by a trusted Certificate Authority (CA).
```

## Guided Steps

### Step 1 - Identify the Destination and Observation

1. Open your browser and visit `https://example.com`. Do not sign in or enter a password.
2. Look at the address after the page loads. Sometimes one address sends you to another; that is a **redirect**. Write the name you ended up visiting in the table.
3. Record today’s date, time, and time zone. A time zone tells us which local clock you used.
4. Open the site-information button beside the address. Look for connection or certificate information. Wording may include “Connection is secure” or “Certificate is valid.”
5. Open the certificate details. Browser menus differ. If you cannot find them, ask your instructor to show you. Do not install anything.

**What you should see:** information about the website’s certificate. Copy the browser’s message exactly. For the browser version, use its Help/About screen if available; ask for help if needed.

| Observation | Your record |
| --- | --- |
| Starting public URL | https://www.iana.org/help/example-domains |
| Final expected hostname | www.iana.org |
| Observation date and time | 9/28/2026 12:37AM  |
| Time zone | EST |
| Browser and version | Google Chrome Version 153.0.8010.36 (Official Build) (64-bit) |
| Browser connection/certificate status, exactly as shown | Connection is secure/ Common Name (CN)	www.iana.org Organization (O)	<Not Part Of Certificate> Organizational Unit (OU)	<Not Part Of Certificate> Common Name (CN)	WE1 Organization (O)	Google Trust Services Organizational Unit (OU)	<Not Part Of Certificate> Issued On	Friday, August 21, 2026 at 4:51:32 PM Expires On	Thursday, November 19, 2026 at 4:51:30 PM Certificate	cbf3a200a42e2b6b751fb6beb6d1b72a464a0ab7ffebfca0fff071af2c185b64 Public Key	bdc3ea4b292dd9f040d9218cab668bd8c391efd6b9cae6e3c79c98507d6e2eae |

If a warning appears, stop before proceeding to the site. Record the warning privately and select an approved alternative with your instructor. A warning is not a request to disable verification.

### Step 2 - Read the Leaf Certificate

Select the certificate for the website itself. This is called the **leaf certificate** because it is at the end of the signing chain. Other certificates in the list belong to the offices that issued certificates.

Open Details or Fields. A **field** is one labeled piece of information, like “Name” on a badge. Work down the table one row at a time. Use this guide to understand the labels:

| Label in the viewer | Plain-language meaning |
|---|---|
| Subject | Who or what this certificate describes. |
| Subject Alternative Name (SAN) | The list of website names the certificate covers. Use this list to check the name you visited. |
| Issuer | The office that signed this certificate. Such an office is called a certificate authority, or **CA**. |
| Not Before / Not After | The start and end of the certificate’s allowed date-and-time period. |
| Subject public-key algorithm and size | The kind of public key and its size. An **algorithm** is a set of instructions for doing a calculation. Copy the label and number you see. |
| Certificate signature algorithm | The method the issuing office used to sign the certificate. This is a different job from the website’s own public key. |
| Extended Key Usage (EKU) | The listed jobs for this certificate, such as identifying a web server. |
| Basic Constraints | Whether this certificate may act as an issuing office (CA). |
| Serial number / SHA-256 fingerprint | A tracking number, or a calculated fingerprint, that helps identify the particular certificate you inspected. |

You do not need to explain how the algorithms work. In the last column below, explain the field’s job in your own words. Expand a long list to see its entries. A Subject “Common Name” is not a substitute for checking the SAN list.

| Field | Value you observed | What question does this field help answer? |
| --- | --- | --- |
| Subject | www.iana.org | Which specific hostnames or web addresses is this certificate valid to protect? |
| Subject Alternative Name (SAN) | www.iana.org | Which specific hostnames or web addresses is this certificate valid to protect? |
| Issuer | WE1, Google Trust Services | Which trusted certificate authority (CA) issued and signed this certificate? |
| Not Before | Friday, August 21, 2026 at 4:51:32 PM | What is the earliest date and time this certificate becomes valid for use? |
| Not After | Thursday, November 19, 2026 at 4:51:30 PM | When does this certificate expire and cease to be valid? |
| Subject public-key algorithm and size, if shown | bdc3ea4b292dd9f040d9218cab668bd8c391efd6b9cae6e3c79c98507d6e2eae | What cryptographic algorithm and key length does the website use for its public key? |
| Certificate signature algorithm | not observed | What algorithm did the issuing office use to sign and secure this certificate? |
| Extended Key Usage (EKU), if shown | not observed | What specific roles or purposes is this certificate permitted to perform? |
| Basic Constraints, if shown | not observed | Is this certificate allowed to act as an issuing authority (CA) to sign other certificates? |
| Serial number or SHA-256 certificate fingerprint | cbf3a200a42e2b6b751fb6beb6d1b72a464a0ab7ffebfca0fff071af2c185b64 | What unique tracking identifier or digital fingerprint distinguishes this specific certificate? |

Copy the matching SAN entry fully. If other names are listed, say “additional names listed.” Keep the website’s public-key information separate from the method used to sign its certificate.

**If you cannot find a field:** write “not observed” and ask your instructor. If you have confirmed that the full certificate has no EKU field, write “extension not present.” Not seeing a label in a limited viewer does not prove it is missing from the certificate.

### Step 3 - Check the Website Name and Dates

Now do two badge checks yourself: “Right name?” and “Still within its dates?” A wildcard is a `*` that stands in for part of a name.

1. Compare your final expected hostname with the leaf's DNS SAN entries. For a wildcard, `*.example.com` ordinarily matches one label such as `shop.example.com`, not `example.com` or `a.shop.example.com`.
2. Compare the observation time with Not Before and Not After using consistent time zones. Do not change your device clock.
3. Record the browser result separately from the field comparison.

```text
Expected hostname: "Right name? (SAN Entry Match)
Leaf DNS SAN Entries: DNS Name: www.iana.org, DNS Name iana.org
Evaluation: PASS. The expected hostname www.iana.org matches the DNS SAN entry www.iana.org exactly.
Observation Time: September 24, 2026 at 19:32:54 CEST (17:32:54 UTC)
Not Before: August 21, 2026 at 16:51:32 UTC (18:51:32 CEST)
Not After: November 19, 2026 at 16:51:30 UTC (18:51:30 CEST)
Evaluation: PASS. Using a consistent time zone (UTC/CEST), September 24, 2026 falls directly between the Not Before date (August 21, 2026) and the Not After date (November 19, 2026). The certificate is active and not expired.
Matching SAN entry, or no match: www.iana.org
Why the entry matches or does not match: The entry matches because the final expected hostname visited (www.iana.org) exactly matches the www.iana.org Fully Qualified Domain Name (FQDN) explicitly listed in the certificate's Subject Alternative Name (SAN) extension.
Observation time and certificate time zone: 9/28/2026 8:44 PM EST (Observation time) and UTC / GMT (Certificate validity time zone).
Is your observation time between the start and end dates? Explain: Yes, the observation time falls between the start and end dates.
When converted to the same time zone (UTC), September 21, 2026, is well after the Not Before date of August 21, 2026, and well before the Not After date of November 19, 2026. Therefore, the certificate was active and valid at the time of observation.
Browser-reported result: Connection is secure" / "Certificate is valid" (Google Chrome reported a valid, trusted connection to www.iana.org with no certificate warnings or errors).
What I checked myself versus what the browser reported: I independently verified that the destination hostname (www.iana.org) directly matched the domain name listed in the certificate’s Subject Alternative Name (SAN) extension and confirmed that our observation time fell within the certificate’s valid Not Before and Not After window. Conversely, the browser reported that the overall connection was secure and the certificate was valid, indicating that it successfully performed automated background checks—such as validating the full cryptographic signature chain up to a trusted Root CA and checking for revocation which I did not perform manually.
```

### Step 4 - Map the Observed Chain

Look for a view called **hierarchy**, **certification path**, or **chain**. These are names for the list of certificates linked by signatures.

Think of a badge office approved by a larger office:

- **Leaf:** the website’s badge.
- **Intermediate:** an issuing office between the website and the top office. There can be more than one, or none shown.
- **Root / trust anchor:** the top office your browser is set up to accept. A **client** is the program doing the checking; here, that is your browser.

Record only what your browser shows. The browser may add a root from its own stored list. This screen is not a recording of everything the website sent. Also, reading matching office names is not the same as doing the mathematical signature checks yourself.

| Position / role | Subject | Issuer | Where observed | What remains unknown? |
| --- | --- | --- | --- | --- |
| Leaf / website | www.iana.org | WE1 | Browser Certificate Viewer Leaf Certificate Details | Whether the server sent intermediate certificates directly or if Chrome fetched them via AIA. |
| Intermediate, if shown | WE1 | GTS Root R1 | Browser Certificate Viewer Hierarchy View | Whether this intermediate CA has undergone recent unannounced policy or operational changes. |
| Additional intermediate, if shown | Not Shown | Not Shown | Not Shown | Additional intermediate |
| Root / trust anchor, if shown | GTS Root R1 | GTS Root R1 | Browser Certificate Viewer | Whether other client devices or legacy operating systems trust this root CA. |

Remove unused intermediate rows or mark them “not shown.” Do not invent a three-certificate chain. If the viewer exposes only the leaf, report that limit and ask the instructor for a supported viewer demonstration.

Make a simple labeled chain sketch, or write the relationship in words:

```text
The website leaf is signed by: WE1 Google Trust Services Intermediate CA
That issuer is signed by (if shown): GTS Root R1
The top office (root / trust anchor) shown by my browser is (or not observed): GTS Root R1
Why an office signing its own badge is not enough (who must choose to accept that office?): CN = GTS Root R4
O = Google Trust Services LLC
C = US
This view is the browser's displayed path; I have / have not independently captured what the server sent: I have not independently captured what the server sent.
Reason the browser's certificate viewer displays the constructed validation path built by the browser—which may fetch intermediate certificates automatically—rather than raw packet data captured from the TLS handshake using network tools like Wireshark or OpenSSL.
```

## Stop & Check

- Is the selected certificate the website leaf, rather than its CA?
- Did you distinguish the subject key from the issuer's signature algorithm?
- Did you record the actual observation date and time zone?
- Did you label a field you could not see as “not observed”?
- Did you explain why an office signing its own badge does not make everyone accept that office?

## Test

Your test is to compare the name and dates, then record the browser’s result. Write “I checked…” for your own work and “The browser reported…” for its result. You have not separately checked every signature yourself. You also have not separately checked whether an issuer canceled the certificate early; that is called **revocation**. Do not claim checks you did not perform.

## Capture Evidence

Capture the expanded leaf fields and the chain/hierarchy view. Use additional numbered images when one image cannot show all fields legibly. Include captions describing what each screenshot proves. Keep account details and browser address bars outside the crop.

## Explain

Write 3–4 sentences using the visitor-badge example. Explain one field, who signed the website’s certificate, why the browser accepts the top office, and one thing a certificate cannot promise. Sentence starters: “The SAN list is like…”, “The issuing office…”, “My browser accepts…”, and “This does not mean…”.

```text
The SAN list is like a list of authorized destinations printed on a visitor's badge, specifying the exact website hostnames the certificate is approved to cover. The issuing office that signed the website's certificate is WE1, an intermediate certificate authority operated by Google Trust Services. My browser accepts the top office, GTS Root R1, because its root certificate is pre-installed and explicitly trusted in the browser's local trust store. This does not mean, however, that the website's content, downloads, or intentions are guaranteed to be safe—it only proves that the identity and encrypted connection are verified by a recognized authority.
```

## Required Evidence

Save screenshots in `assets/screenshots/week-09/`:

- `week09-lab01-certificate-fields.png` (add `-02`, `-03` if needed)
- `week09-lab01-chain-view.png`

Complete all observation, field, name/time, and chain records in this worksheet. A chain sketch can be embedded as `week09-lab01-chain-map.png` or written in the provided fields. Browser-specific layouts and live certificate changes are acceptable when the evidence is internally consistent.

### Evidence Upload - Certificate Fields (required)

**Caption - certificate fields:** General tab on the certificate

### Evidence Upload - Chain View (required)

**Caption - chain view:** www.iana.org, here is the trust chain hierarchy for the site's certificate

### Optional Extra Evidence (leave blank if you do not need it)

**Caption - extra certificate fields image:** week09-lab01-certificate-fields-02 through 22 WE1 Certificate fields

**Caption - third certificate fields image:** week09-lab01-certificate-fields-23 through 46 www.iana.org certificate fields

**Caption - chain sketch image:** Chain sketch of www.iana.org, here is the trust chain hierarchy for the site's certificate

## Analysis Questions

**Analysis Question 1.** Ivy has two working keys with the same label. Why does a working key or a correct signature not, by itself, prove that the key belongs to the support team? Write at least 3 sentences.

```text
A key label is arbitrary plain text that anyone can edit or apply to any key pair, so a match in label text carries no cryptographic proof of identity. Furthermore, a valid signature or working key only proves that a mathematically corresponding public/private key pair was used to sign or encrypt data—it does not prove who actually generated, controls, or owns that key pair. Without a verification mechanism like a digital certificate issued and digitally signed by a trusted Certificate Authority (CA) or a established out-of-band web of trust, there is no inherent cryptographic link tying the public key to the genuine support team.
```

**Analysis Question 2.** Anyone could print an office name on a badge. Why must the browser check more than the printed issuer name? Explain how the browser’s settings or accepted list determines which top offices it trusts. Write at least 3 sentences.

```text
Simply reading a printed issuer name on a certificate is not enough because any untrusted party can write a legitimate-sounding authority name on a fake certificate. To prevent impersonation, the browser must cryptographically verify the digital signature embedded in the certificate using the issuer’s actual public key. The browser relies on a pre-installed, secure local "Trust Store" (or accepted root list), which contains the verified public keys of trusted Root Certificate Authorities (CAs). If a certificate's chain of digital signatures does not trace back to one of these explicitly trusted top offices in the browser's settings, the browser flags the certificate as untrusted regardless of what name is written on it.
```

**Analysis Question 3.** What did your name, date, and browser checks tell you about this connection? Why do they not promise that everything the website says or offers is safe? Say which checks you did and which you did not do. Write at least 3 sentences.

```text
My manual checks confirmed that the expected hostname (www.iana.org) exactly matches the SAN entry on the certificate and that the observation date falls within the certificate's active validity period, while the browser confirmed that the cryptographic signature chain is valid and trusted. However, these checks only prove identity and transport-layer encryption; they do not guarantee that the website's content, downloads, or intentions are safe or free from malware. I explicitly performed the domain name matching, date/time validity comparison, and certificate field inspection myself, but I did not independently capture the raw TLS handshake packets, perform manual cryptographic signature verification, or check real-time certificate revocation status (OCSP/CRL).
```

## Submission Checklist

- [x] Public hostname, observation time, time zone, and browser recorded

- [x] Certificate fields completed, with unavailable fields labeled honestly

- [x] SAN/name and validity comparisons explained

- [x] Observed chain roles mapped without inventing missing certificates

- [x] Browser-reported result distinguished from my own inspection

- [x] Both required screenshot subjects captured clearly

- [x] Analysis answers completed in my own words

- [x] No credentials, private keys, account details, or Bastion URL included

- [x] Worksheet saved to `week-09/labs/lab-01-investigate-a-certificate.md`

## GitHub / Lab Portal Submission

A **repository** is your project’s folder on GitHub. A **commit** is a saved set of changes. A `.md` file is a text document that uses simple formatting marks. Keep the headings and fill in the blank answers.

1. Complete this worksheet on this page, then press **Save Progress**. Your answers are stored in the portal and reload the next time you open this lab.
2. Press **Submit to GitHub**. The portal writes the finished worksheet to the submission path above in your connected portfolio repository. If you have not connected GitHub yet, the portal will ask you to connect and pick your repository first.
3. Add the reviewed screenshot addresses in the evidence fields above, or upload the images under `assets/screenshots/week-09/` in your portfolio repository.
4. Open the committed worksheet and every image on GitHub. Confirm that tables render, images are legible, and private information is absent.
5. Keep this investigation for Portfolio Deliverable 3 and Lab 02's comparison.

*CyberVisionaries Institute · CyberFoundations · Tier I*
