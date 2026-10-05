# Week 9 Notes - Vault Exchange Digital Trust

**Student Name:** Dan Martinson

**Week:** 9

Use your own words. Short notes and everyday examples are welcome. You do not need to memorize commands.

## From a Key to an Identity

Ivy has two keys with the same label. Why is the label not enough? How can checking a visitor badge help explain the problem?

```text
My explanation: Why the label isn't enough:
A label on a key is just self-reported text—anyone can write "Server Key" on a piece of metal, but that doesn't prove who actually created it or whether it's legitimate. If I'm holding two keys with identical labels, I have no way to verify which one truly belongs to the authorized server owner and which one might be an untrusted copy or an imposter key meant to compromise security.

How a visitor badge explains the problem:
I like to think of a simple key label like a sticky note name tag that says "Tom." Anyone can write "Tom" on a piece of paper and slap it on their shirt, but it proves nothing about who they really are.

A visitor badge fixes this problem because it binds an identity to a set of verifiable details—it includes a full name, photo, expiration date, and most importantly, it is issued and signed by a trusted security office. By checking the badge, I'm not just taking the person's word for it; I'm relying on a trusted authority who vetted them. In digital security, a certificate acts as that visitor badge: it securely binds a cryptographic key to a verified identity, so I know exactly who I'm connecting to.
```

## Certificate Fields

A certificate is a digital badge. Explain the name list (SAN), signing office (issuer), start/end dates, public key, signature method, and allowed job (purpose). Which field would you check to see whether the badge covers the right website?

```text
Field and its job: Here is how I would explain each certificate field in my own words using the visitor badge analogy:
Name List (SAN - Subject Alternative Name): I check this field to see the exact list of web domain names authorized to use this certificate, similar to how a visitor badge lists the specific buildings or rooms I am permitted to enter.
Signing Office (Issuer): This field shows the trusted Certificate Authority (CA) that verified the website's identity and stamped the certificate, just like the official security department that created and signed a visitor badge.
Start/End Dates (Validity Period): This timeframe tells me when the certificate is active and trustworthy, acting exactly like an expiration date printed on a badge to prevent old credentials from being used indefinitely.
Public Key: This is the shareable cryptographic key bound to the certificate, functioning like the photo printed on my visitor badge so anyone can verify that the badge matches the server holding it.
Signature Method: This specifies the exact cryptographic algorithm used to secure the certificate, which acts like a special anti-counterfeiting seal or hologram stamped on a physical badge to prevent tampering.
Allowed Job (Key Usage / Extended Key Usage): This field defines the precise role the certificate can perform (such as Server Authentication), which is like printing "Contractor" or "Guest" on a badge to ensure it isn't misused for an unauthorized purpose.
To see whether the badge covers the right website, I would check the Name List (SAN) field to confirm that the website's address is explicitly listed.
```

## Issuers and Accepted Trust

Who signed the badge? Who chooses whether to accept the top office? Explain why an office signing its own badge is not enough to make your browser trust it.

```text
My explanation: Who signed the badge?
The badge (the certificate) is signed by the Issuer, which is a Certificate Authority (CA) or an Intermediate CA acting as the signing office. The issuer uses its own private key to cryptographically seal the certificate's details, confirming that the public key belongs to the verified entity.
Who chooses whether to accept the top office?
My browser, operating system, or application environment determines whether to trust the top office (the Root CA). Software vendors maintain a built-in, strictly vetted database called a trust store (or root store). If a Root CA's self-signed certificate is explicitly included in my device's local trust store, my browser will accept it as a root of trust.
Why an office signing its own badge is not enough to make my browser trust it:
An entity signing its own badge produces a self-signed certificate. Anyone can generate a key pair and issue a self-signed badge claiming to represent any domain name, such as google.com or bank.com. While a self-signed badge proves mathematical ownership of the corresponding private key, it offers zero third-party identity verification. If my browser accepted self-signed certificates by default, an attacker could easily execute a Man-in-the-Middle (MitM) attack by generating their own self-signed badge to impersonate legitimate services and intercept encrypted traffic. Browsers require a verifiable chain of trust originating from an established, pre-approved Root CA in their trust store.
```

## Key CSR and Certificate Roles

The CSR is a badge application. Explain the separate jobs of the service’s private key, application, office’s private key, and finished certificate. Who signs the application? Who signs the finished badge?

```text
My explanation: Separate Jobs of Each Component:
Service’s Private Key: This key remains strictly secret on the server. Its primary job is to prove ownership during the TLS handshake by decrypting or signing data and to sign the initial CSR application to prove possession of the key pair.
Application (CSR - Certificate Signing Request): The formal, standardized application sent to a Certificate Authority. It contains the service's public key, identity information (such as domain names/SAN), and proof of private key ownership.
Office’s Private Key (CA Private Key): The highly guarded, confidential key held by the Certificate Authority (the issuing office). Its sole function is to apply the digital signature that approves and seals the issued certificate, extending trust to the applicant.
Finished Certificate: The publicly shareable digital credential issued by the CA. It binds the server’s identity and public key together under the CA's trusted digital signature, allowing client browsers to verify authentic connections.
Who Signs What?
Who signs the application (CSR)? The applicant (the service owner) signs the CSR using the service's private key to prove they possess the private key corresponding to the public key submitted in the request.
Who signs the finished badge (Certificate)? The issuing authority (the CA) signs the final certificate using the office's private key (CA private key) to cryptographically attest to the validity of the certificate's contents.
```

## TLS and Verification Evidence

Compare looking at a certificate, checking its saved file, and connecting to a running service. TLS sets up a protected connection. What did you observe in each activity?

```text
I looked at: I inspected the static text and metadata fields of a certificate (such as using openssl x509 -text -noout or browser certificate viewer details). I observed identity claims including the Subject Alternative Name (SAN), Issuer, Validity Dates, Public Key parameters, and Signature Algorithm. This verified what identity details the certificate claims to represent, but it did not confirm whether the trust chain was valid or whether the live server actually possessed the associated private key.
I checked: I validated a saved certificate file locally against a trust store or intermediate chain using a command line tool (such as openssl verify). I observed whether the static certificate file was structurally sound, unexpired, and cryptographically signed by a trusted Certificate Authority (CA) chain terminating at a root certificate in the trust store. This confirmed local cryptographic validity without making network calls or verifying live server configuration.
I connected to: I initiated an active session to a live service over the network (such as using curl -v, openssl s_client, or a web browser). I observed the complete, dynamic TLS handshake in action—including protocol/cipher suite negotiation, server identity verification, and dynamic proof-of-possession where the server proved ownership of the matching private key. This confirmed that the service was actively listening, correctly configured, and capable of establishing a secure, encrypted connection.
```

## Troubleshooting and Remediation

These words mean finding and fixing a problem. Record an actual message, what it meant, and your next step. Consider a wrong name, expired dates, wrong office, canceled certificate, or service that is not running. Label situations you only discussed; do not claim to have tested them.

```text
Message or situation: connect:errno=111
What it means: This indicates a TCP transport-layer failure where no server process is actively listening on port 8443, causing the operating system kernel to immediately reject the connection attempt before any TLS handshake or certificate checks take place. (Tested live during Lab 02)
What I would check or fix: I would check if the service process is running using ss -ltn 'sport = :8443' and start or restart the listener daemon (e.g., openssl s_server) bound to 127.0.0.1:8443.
Which check I would repeat: I would repeat the socket listener check with ss -ltn 'sport = :8443' to confirm port 8443 is open, followed by the live connection test using openssl s_client.
```

## Questions I Still Have

```text
A word or step I want explained again: I would like a clearer explanation of how real-time certificate cancellation (OCSP stapling vs. Certificate Revocation Lists) works in practice during live web traffic compared to static date checks.
```
