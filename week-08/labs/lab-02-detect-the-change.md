# Week 8 Lab 02 — Detect the Change

**Student Name:** Dan Martinson

**Date Completed:** 9/13/2026

**Module:** 3 — Practical Cryptography  
**Submission Path:** `week-08/labs/lab-02-detect-the-change.md`

> ## STOP — Protect secrets
> Never paste, upload, commit, or screenshot a password, passphrase, or private key. Do not run `cat` on any private-key file. Submit only the worksheet and the named screenshots. Keep all cryptographic files on the VM.

## How to Use This Lab

- **[TERMINAL]** means type or paste the command into the Cloud Heights terminal.
- **[WORKSHEET]** means type your response in this lab worksheet.
- Run commands in the order shown. Do not type the sample output.
- If your result does not match the stated success check, stop at the Troubleshooting box. Do not improvise with `sudo`, package installation, Azure settings, or SSH server configuration.

## Mission

Create a SHA-256 fingerprint of the original report, change a copy, and prove that the changed copy has a different fingerprint.

## What You Already Know

A cryptographic hash produces a fixed-length digest. Hashing does not hide content and has no decrypt step. A mismatch proves the two inputs differ; it does not identify who made the change.

## Lab Environment / Pre-Lab Check

**[TERMINAL] Run:** analyst@cf-student-07:~$ whoami analyst analyst@cf-student-07:~$ cf-week-check cf-week-check: command not found analyst@cf-student-07:~$ cfweek8-check cfweek8-check: command not found analyst@cf-student-07:~$ cf-week8-check [PASS] analyst account [PASS] openssl [PASS] sha256sum [PASS] SSH client [PASS] SSH server [PASS] xxd [PASS] tree [PASS] file [PASS] cmp [PASS] diff [PASS] sshd active [PASS] public-key authentication enabled [PASS] password authentication enabled [PASS] Week 8 workspace [PASS] incident-report.txt [PASS] analyst ownership  SUMMARY: 16 passed, 0 failed analyst@cf-student-07:~$ cd ~/cloud-heights/week8-cryptography analyst@cf-student-07:~/cloud-heights/week8-cryptography$ test -f evidence/incident-report.txt && echo "READY: starting file exists" READY: starting file exists analyst@cf-student-07:~/cloud-heights/week8-cryptography$

```bash
whoami
cf-week8-check
cd ~/cloud-heights/week8-cryptography
test -f evidence/incident-report.txt && echo "READY: starting file exists"
```

**Continue only if:** `whoami` prints `analyst`, all checks report `PASS`, and the final line is `READY: starting file exists`.

### If the VM Stops

Return to **My Lab Environment** in the Lab Portal and start your assigned VM. A stopped or deallocated VM is not deleted; saved disk files remain.

## Predict First

**[WORKSHEET]** If one line is added to a file, will its SHA-256 digest remain the same? Explain.

```text
No, the SHA-256 digest will not remain the same; it will change completely
Here is why.
Cryptographic Hash Properties: A cryptographic hash function like SHA-256 takes all input bytes from a file and processes them to create a unique, fixed-length digest.

The Avalanche Effect: Even a microscopic modification to a file—such as adding a single character, space, or new line—causes a drastic, unpredictable change across the entire output hash.

Integrity Detection: Because the hash is calculated across the whole file, any modification alters the input mathematical state, resulting in a completely different digest. This allows security systems to instantly verify if a file's integrity has been compromised.

```

## Guided Steps

### Step 1 — Hash the Original

**[TERMINAL] Run:** analyst@cf-student-07:~/cloud-heights/week8-cryptography$ sha256sum evidence/incident-report.txt | tee hashes/original.sha256 2730c699c92e14b197c73e56191170b4e20de9d42354acf313fec63e35b727e1  evidence/incident-report.txt analyst@cf-student-07:~/cloud-heights/week8-cryptography$ ^C analyst@cf-student-07:~/cloud-heights/week8-cryptography$

```bash
sha256sum evidence/incident-report.txt | tee hashes/original.sha256
```

**Expected result:** A 64-character hexadecimal digest followed by the original filename.

### Step 2 — Create and Change a Copy

**[TERMINAL] Run:** analyst@cf-student-07:~/cloud-heights/week8-cryptography$ cp evidence/incident-report.txt hashes/incident-report-modified.txt analyst@cf-student-07:~/cloud-heights/week8-cryptography$ cp evidence/incident-report.txt hashes/incident-report-modified.txt analyst@cf-student-07:~/cloud-heights/week8-cryptography$ echo "Review Note: Integrity validation exercise completed." >> hashes/incident-report-modified.txt analyst@cf-student-07:~/cloud-heights/week8-cryptography$ echo "Review Note: Integrity validation exercise completed." >> hashes/incident-report-modified.txttail -n 3 hashes/incident-report- modified.txttail -n 3 hashes/incident-report-modified.txt analyst@cf-student-07:~/cloud-heights/week8-cryptography$ tail -n 3 hashes/incident-report-modified.txt Status: Pending Security Analyst review. Review Note: Integrity validation exercise completed.

```bash
cp evidence/incident-report.txt hashes/incident-report-modified.txt
echo "Review Note: Integrity validation exercise completed." >> hashes/incident-report-modified.txt
tail -n 3 hashes/incident-report-modified.txt
```

**Expected result:** The added `Review Note` appears in the last three lines. The original file was not changed.

### Step 3 — Hash the Changed Copy

**[TERMINAL] Run:** analyst@cf-student-07:~/cloud-heights/week8-cryptography$ sha256sum hashes/incident-report-modified.txt | tee hashes/modified.sha256 3d29a99ae617fcb6dc84f567284fb74d653a7606ba19c97f02018be929c0b88c  hashes/incident-report-modified.txt analyst@cf-student-07:~/cloud-heights/week8-cryptography$ ^C analyst@cf-student-07:~/cloud-heights/week8-cryptography$

```bash
sha256sum hashes/incident-report-modified.txt | tee hashes/modified.sha256
```

### Step 4 — Compare the Digest Values

**[TERMINAL] Run:** analyst@cf-student-07:~/cloud-heights/week8-cryptography$ ORIGINAL_HASH=$(cut -d' ' -f1 hashes/original.sha256) analyst@cf-student-07:~/cloud-heights/week8-cryptography$ MODIFIED_HASH=$(cut -d' ' -f1 hashes/modified.sha256) analyst@cf-student-07:~/cloud-heights/week8-cryptography$ printf 'ORIGINAL: %s > ' "$ORIGINAL_HASH" "$MODIFIED_HASH" ORIGINAL: c00d49d7261c0e666252d41139c01405c735d1d9ba926efd1edc97145d45f179 ORIGINAL: 96ea688ae679eb5cd9bb30717ea0612c2c5283aa15d2ed9f3ed4d74a199d186b analyst@cf-student-07:~/cloud-heights/week8-cryptography$ echo "EXPECTED: hashes differ because the file changed" EXPECTED: hashes differ because the file changed analyst@cf-student-07:~/cloud-heights/week8-cryptography$

```bash
ORIGINAL_HASH=$(cut -d' ' -f1 hashes/original.sha256)
MODIFIED_HASH=$(cut -d' ' -f1 hashes/modified.sha256)
printf 'ORIGINAL: %s
MODIFIED: %s
' "$ORIGINAL_HASH" "$MODIFIED_HASH"
if [ "$ORIGINAL_HASH" = "$MODIFIED_HASH" ]; then
  echo "UNEXPECTED: hashes match — stop and troubleshoot"
else
  echo "EXPECTED: hashes differ because the file changed"
fi
```

**Required result:** Two different digest values and `EXPECTED: hashes differ because the file changed`.

**Evidence moment:** Capture the terminal now as `week08-lab02-sha256-comparison.png`.

## Stop & Check

If you see `UNEXPECTED`, do not submit.

### Troubleshooting

Run `tail -n 3 hashes/incident-report-modified.txt`. If the Review Note is missing, repeat Step 2 once, then repeat Steps 3–4. Do not edit the original file.

## Explain

**[WORKSHEET]** In 3–4 sentences, state what the mismatch proves and two things it does not prove.

```text
The hash mismatch proves that the modified file is no longer byte-for-byte identical to the original report, meaning its content was altered. However, it does not prove who made the change because hashing only tracks data integrity, not user identity or authorization. It also does not prove what specific changes were made or whether the edit was intentional, accidental, or malicious.
```

## Analysis Questions

1. What does the different SHA-256 value prove?

```text
It proves that the contents of the file were changed and it's no longer byte-for-byte identical to the original version. It guarantees that the data's integrity was compromised, showing that at least one byte was altered, added, or deleted.
```

2. Why does the mismatch not identify the person who changed the file?

```text
A hash function is a one-way mathematical algorithm that operates strictly on the data inside the file, not on external metadata or user credentials.

Because the hash function only calculates a digest based on the file's raw bytes, it only detects that the data has changed. It does not record or embed contextual details such as user IDs, IP addresses, system timestamps, or digital signatures that would link the modification to a specific person.
```

3. Why does hashing not protect confidentiality?

```text
Hashing does not protect confidentiality because it is not encryption—it doesn't scramble data to hide it from unauthorized readers.
Hashes do not obscure the original data: Generating a hash creates an additional fixed-length output, a digest, but it does nothing to modify, hide, or protect the original file. If someone opens or reads the file, the contents remain fully visible in plaintext.

Hashes are deterministic: The same input always produces the same hash digest. If an attacker knows a list of possible inputs, such as common passwords, they can hash them all in advance and compare the hashes to easily guess the hidden data.

Hashing is designed to verify integrity (showing if data was altered), not confidentiality (keeping data secret).
```

## Required Evidence

- `assets/screenshots/week-08/week08-lab02-sha256-comparison.png`

## Submission Checklist

- [x] The original and changed copy have different digests.

- [ ] The required success message appears.

- [x] The screenshot uses the exact filename.

- [x] The original evidence file was not modified.

- [x] Every worksheet response is complete.

## GitHub / Lab Portal Submission

1. In the Lab Portal, open the matching Week 8 lab.
2. Complete every **[WORKSHEET]** response.
3. Upload only the required screenshots to `assets/screenshots/week-08/`.
4. Select **Submit to GitHub**.
5. Open the committed worksheet and screenshots on GitHub. Confirm they are readable and contain no secrets.

**Never submit:** `.pem` files, files from `~/.ssh/`, passwords, passphrases, private-key contents, or a Bastion shareable URL.
