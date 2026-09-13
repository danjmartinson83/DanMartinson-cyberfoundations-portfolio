# Week 8 Lab 01 — Protect the Incident File

**Student Name:** Dan Martinson

**Date Completed:** 9/12/2026

**Module:** 3 — Practical Cryptography  
**Submission Path:** `week-08/labs/lab-01-protect-the-incident-file.md`

> ## STOP — Protect secrets
> Never paste, upload, commit, or screenshot a password, passphrase, or private key. Do not run `cat` on any private-key file. Submit only the worksheet and the named screenshots. Keep all cryptographic files on the VM.

## How to Use This Lab

- **[TERMINAL]** means type or paste the command into the Cloud Heights terminal.
- **[WORKSHEET]** means type your response in this lab worksheet.
- Run commands in the order shown. Do not type the sample output.
- If your result does not match the stated success check, stop at the Troubleshooting box. Do not improvise with `sudo`, package installation, Azure settings, or SSH server configuration.

## Mission

Encrypt a readable incident report, inspect the encrypted file safely, decrypt it, and prove the recovered file is identical to the original.

## What You Already Know

Encryption changes readable **plaintext** into protected **ciphertext**. In this lab, one passphrase protects and recovers the file. Encryption supports confidentiality, but it does not prevent someone from deleting or copying the encrypted file.

## Lab Environment / Pre-Lab Check

| Item | Required value |
|---|---|
| VM | Your assigned `cf-student-XX` VM |
| Linux account | `analyst` |
| Working directory | `~/cloud-heights/week8-cryptography` |
| Starting file | `evidence/incident-report.txt` |
| Estimated time | 25–35 minutes |

**[TERMINAL] Run:** analyst@cf-student-07:~$ analyst@cf-student-07:~$ whoami analyst@cf-student-07:~$: command not found analyst@cf-student-07:~$ analyst analyst: command not found analyst@cf-student-07:~$ analyst@cf-student-07:~$ hostname analyst@cf-student-07:~$: command not found analyst@cf-student-07:~$ cf-student-07 cf-student-07: command not found analyst@cf-student-07:~$ analyst@cf-student-07:~$ cf-week8-check analyst@cf-student-07:~$: command not found analyst@cf-student-07:~$ [PASS] analyst account [PASS]: command not found analyst@cf-student-07:~$ [PASS] openssl [PASS]: command not found analyst@cf-student-07:~$ [PASS] sha256sum [PASS]: command not found analyst@cf-student-07:~$ [PASS] SSH client [PASS]: command not found analyst@cf-student-07:~$ [PASS] SSH server [PASS]: command not found analyst@cf-student-07:~$ [PASS] xxd [PASS]: command not found analyst@cf-student-07:~$ [PASS] tree [PASS]: command not found analyst@cf-student-07:~$ [PASS] file [PASS]: command not found analyst@cf-student-07:~$ [PASS] cmp [PASS]: command not found analyst@cf-student-07:~$ [PASS] diff [PASS]: command not found analyst@cf-student-07:~$ [PASS] sshd active [PASS]: command not found analyst@cf-student-07:~$ [PASS] public-key authentication enabled [PASS]: command not found analyst@cf-student-07:~$ [PASS] password authentication enabled [PASS]: command not found analyst@cf-student-07:~$ [PASS] Week 8 workspace [PASS]: command not found analyst@cf-student-07:~$ [PASS] incident-report.txt [PASS]: command not found analyst@cf-student-07:~$ [PASS] analyst ownership [PASS]: command not found analyst@cf-student-07:~$  analyst@cf-student-07:~$ SUMMARY: 16 passed, 0 failed SUMMARY:: command not found analyst@cf-student-07:~$ analyst@cf-student-07:~$ pwd analyst@cf-student-07:~$: command not found analyst@cf-student-07:~$ /home/analystpwd -bash: /home/analystpwd: No such file or directory analyst@cf-student-07:~$ whoami analyst analyst@cf-student-07:~$ hostname cf-student-07 analyst@cf-student-07:~$ cf-week8-check [PASS] analyst account [PASS] openssl [PASS] sha256sum [PASS] SSH client [PASS] SSH server [PASS] xxd [PASS] tree [PASS] file [PASS] cmp [PASS] diff [PASS] sshd active [PASS] public-key authentication enabled [PASS] password authentication enabled [PASS] Week 8 workspace [PASS] incident-report.txt [PASS] analyst ownership  SUMMARY: 16 passed, 0 failed analyst@cf-student-07:~$ cd ~/cloud-heights/week8-cryptography analyst@cf-student-07:~/cloud-heights/week8-cryptography$ pwd /home/analyst/cloud-heights/week8-cryptography analyst@cf-student-07:~/cloud-heights/week8-cryptography$

```bash
whoami
hostname
cf-week8-check
cd ~/cloud-heights/week8-cryptography
pwd
```

**Continue only if:** `whoami` prints `analyst`, the hostname begins with `cf-student-`, every environment check reports `PASS`, and `pwd` ends with `/cloud-heights/week8-cryptography`.

### If the VM Stops

Return to **My Lab Environment** in the Lab Portal and start your assigned VM. A stopped or deallocated VM is not deleted; saved disk files remain.

## Predict First

**[WORKSHEET]** What do you expect to see when encrypted data is inspected as bytes? Why should it not look like the original report?

```text
When inspecting encrypted data as bytes, I expect to see pseudo-random hexadecimal output and garbled binary characters rather than readable ASCII text. It should not look like the original report because the encryption process uses a mathematical cipher and key to scramble the plaintext into ciphertext. This eliminates recognizable patterns and structure, ensuring the report's content remains confidential without the proper decryption key.
```

## Guided Steps

### Step 1 — Confirm the Original Is Readable

**[TERMINAL] Run:** analyst@cf-student-07:~/cloud-heights/week8-cryptography$ cat evidence/incident-report.txt CLOUD HEIGHTS INCIDENT REPORT Incident ID: CH-CRYPTO-08 Classification: Training Use Owner: Security Operations  Summary: A copy of a Grid Operations incident report was discovered in a shared location. The security team must protect the report, verify whether it changes, and document how cryptographic controls can support confidentiality, integrity, and authentication.  Status: Pending Security Analyst review. analyst@cf-student-07:~/cloud-heights/week8-cryptography$  analyst@cf-student-07:~/cloud-heights/week8-cryptography$ ^C analyst@cf-student-07:~/cloud-heights/week8-cryptography$

```bash
cat evidence/incident-report.txt
```

**Expected result:** A readable report beginning with `CLOUD HEIGHTS INCIDENT REPORT`.

### Step 2 — Encrypt the Report

Choose one temporary lab passphrase that you can re-enter during this lab. Do not write it in the worksheet.

**[TERMINAL] Run:** analyst@cf-student-07:~/cloud-heights/week8-cryptography$ openssl enc -aes-256-cbc -salt -pbkdf2 -iter 100000   -in evidence/incident-report.txt   -out encrypted/incident-report.enc enter AES-256-CBC encryption password:

```bash
openssl enc -aes-256-cbc -salt -pbkdf2 -iter 100000   -in evidence/incident-report.txt   -out encrypted/incident-report.enc
```

At `enter AES-256-CBC encryption password:`, type the passphrase. Nothing may appear while you type; this is normal. Press Enter, type the same passphrase again, and press Enter.

**Expected result:** The prompt returns without an error message.

### Step 3 — Inspect the Encrypted File

**[TERMINAL] Run:** analyst@cf-student-07:~/cloud-heights/week8-cryptography$ file encrypted/incident-report.enc encrypted/incident-report.enc: openssl enc'd data with salted password analyst@cf-student-07:~/cloud-heights/week8-cryptography$ xxd -l 64 encrypted/incident-report.enc 00000000: 5361 6c74 6564 5f5f af0e 78d6 b552 3b92  Salted__..x..R;. 00000010: a098 b281 aa46 e0eb d68f e192 14e9 4586  .....F........E. 00000020: 686a 5cfa 5e78 b7d1 dcb5 81f7 c485 f883  hj\.^x.......... 00000030: 1ffe bf13 fb54 9d25 fb2e e14e 7faf 4a21  .....T.%...N..J! analyst@cf-student-07:~/cloud-heights/week8-cryptography$ ^C analyst@cf-student-07:~/cloud-heights/week8-cryptography$ ^C analyst@cf-student-07:~/cloud-heights/week8-cryptography$

```bash
file encrypted/incident-report.enc
xxd -l 64 encrypted/incident-report.enc
```

**Expected result:** `file` identifies data, and `xxd` displays hexadecimal bytes. The readable incident report does not appear.

**Evidence moment:** Capture the terminal now as `week08-lab01-encrypted-inspection.png`.

### Step 4 — Decrypt the File

**[TERMINAL] Run:** analyst@cf-student-07:~/cloud-heights/week8-cryptography$ openssl enc -d -aes-256-cbc -pbkdf2 -iter 100000   -in encrypted/incident-report.enc   -out encrypted/incident-report-decrypted.txt enter AES-256-CBC decryption password: analyst@cf-student-07:~/cloud-heights/week8-cryptography$ ^C analyst@cf-student-07:~/cloud-heights/week8-cryptography$

```bash
openssl enc -d -aes-256-cbc -pbkdf2 -iter 100000   -in encrypted/incident-report.enc   -out encrypted/incident-report-decrypted.txt
```

Enter the same passphrase from Step 2.

### Step 5 — Prove the Files Match

**[TERMINAL] Run:** analyst@cf-student-07:~/cloud-heights/week8-cryptography$ cmp -s evidence/incident-report.txt encrypted/incident-report-decrypted.txt   && echo "MATCH: decrypted file equals original"   || e cho "MISMATCH: stop and troubleshoot" MATCH: decrypted file equals original analyst@cf-student-07:~/cloud-heights/week8-cryptography$

```bash
cmp -s evidence/incident-report.txt encrypted/incident-report-decrypted.txt   && echo "MATCH: decrypted file equals original"   || echo "MISMATCH: stop and troubleshoot"
```

**Required result:** `MATCH: decrypted file equals original`

**Evidence moment:** Capture the terminal now as `week08-lab01-decryption-match.png`.

## Stop & Check

Do not submit unless both required evidence moments succeeded.

### Troubleshooting

- `bad decrypt` or `bad password read`: rerun Step 4 and enter the exact Step 2 passphrase.
- `No such file or directory`: run `cd ~/cloud-heights/week8-cryptography`, then rerun the failed step.
- `MISMATCH`: delete only the decrypted copy with `rm -f encrypted/incident-report-decrypted.txt`, then repeat Steps 4–5.

## Explain

**[WORKSHEET]** In 3–4 sentences, explain how this lab demonstrates confidentiality and why encryption does not prevent deletion.

```text
This lab demonstrates confidentiality by using AES-256 encryption to scramble the readable incident report into ciphertext, making the contents unreadable without the correct passphrase. When inspecting the file as raw bytes, the plaintext patterns are completely hidden, ensuring only authorized parties with the key can view the sensitive data. However, encryption only protects data confidentiality and content secrecy; it does not protect system-level file permissions. Because operating system controls govern file storage, anyone with write or delete permissions on the host system can still erase or overwrite the encrypted file regardless of whether they hold the decryption key.
```

## Analysis Questions

1. Why can an encrypted file still be copied or deleted?

```text
An encrypted file can still be copied or deleted because encryption only protects the contents of the file, not the file system container itself. The operating system handles actions like copying, moving, or deleting files based on directory and file permissions, not on whether the data inside is encrypted or readable. As long as a user account has the necessary write or execute permissions on the host system, the OS will allow them to copy or delete the file container regardless of whether they have the decryption key.
```

2. What job did the passphrase perform?

```text
The passphrase acted as the secret key used by OpenSSL to handle both the encryption and decryption processes. During encryption, it worked with PBKDF2 to derive the cryptographic key and initialization vector that scrambled the cleartext report into unreadable ciphertext. During decryption, entering the exact same passphrase provided the secret needed to reverse the mathematical algorithm and restore the file back to its original readable plaintext.
```

3. Why does the match test prove correct recovery but not prove who handled the file?

```text
The match test proves correct recovery because it compares the decrypted file against the original plaintext byte-for-byte and confirms they are identical, showing that the data was restored without any loss or corruption.

However, it does not prove who handled the file because symmetric encryption and file comparison commands only verify data integrity and content recovery, not identity. The cmp command only looks at the file bytes and does not record user metadata, audit logs, or digital signatures to prove who actually ran the decryption command or accessed the file.
```

## Required Evidence

Save exactly these files in `assets/screenshots/week-08/`:

- `week08-lab01-encrypted-inspection.png`
- `week08-lab01-decryption-match.png`

## Submission Checklist

- [x] Both required results appeared.

- [x] Both screenshots use the exact filenames above.

- [x] No passphrase or other secret appears.

- [x] Every worksheet response is complete.

- [x] The worksheet is saved at the stated submission path.

## GitHub / Lab Portal Submission

1. In the Lab Portal, open the matching Week 8 lab.
2. Complete every **[WORKSHEET]** response.
3. Upload only the required screenshots to `assets/screenshots/week-08/`.
4. Select **Submit to GitHub**.
5. Open the committed worksheet and screenshots on GitHub. Confirm they are readable and contain no secrets.

**Never submit:** `.pem` files, files from `~/.ssh/`, passwords, passphrases, private-key contents, or a Bastion shareable URL.
