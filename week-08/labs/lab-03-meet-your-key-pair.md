# Week 8 Lab 03 — Meet Your Key Pair

**Student Name:** Dan Martinson

**Date Completed:** 9/18/2026

**Module:** 3 — Practical Cryptography  
**Submission Path:** `week-08/labs/lab-03-meet-your-key-pair.md`

> ## STOP — Protect secrets
> Never paste, upload, commit, or screenshot a password, passphrase, or private key. Do not run `cat` on any private-key file. Submit only the worksheet and the named screenshots. Keep all cryptographic files on the VM.

## How to Use This Lab

- **[TERMINAL]** means type or paste the command into the Cloud Heights terminal.
- **[WORKSHEET]** means type your response in this lab worksheet.
- Run commands in the order shown. Do not type the sample output.
- If your result does not match the stated success check, stop at the Troubleshooting box. Do not improvise with `sudo`, package installation, Azure settings, or SSH server configuration.

## Mission

Generate a dedicated Week 8 SSH key pair, identify its two files, and record the public-key fingerprint without exposing the private key.

## What You Already Know

The public and private keys have different jobs. The public key may be shared when appropriate. The private key stays under its owner's control. A key passphrase protects the private-key file; it is not the `analyst` account password.

## Lab Environment / Pre-Lab Check

**[TERMINAL] Run:** Last login: Sat Sep 19 18:46:41 2026 from 192.168.10.134 analyst@cf-student-07:~$ whoami analyst analyst@cf-student-07:~$ cf-week8-check [PASS] analyst account [PASS] openssl [PASS] sha256sum [PASS] SSH client [PASS] SSH server [PASS] xxd [PASS] tree [PASS] file [PASS] cmp [PASS] diff [PASS] sshd active [PASS] public-key authentication enabled [PASS] password authentication enabled [PASS] Week 8 workspace [PASS] incident-report.txt [PASS] analyst ownership  SUMMARY: 16 passed, 0 failed analyst@cf-student-07:~$ test ! -e ~/.ssh/week8_analyst_ed25519 &&   test ! -e ~/.ssh/week8_analyst_ed25519.pub &&   echo "READY: Week 8 key path is unused" ||   echo "STOP: Week 8 key alrea dy exists" READY: Week 8 key path is unused

```bash
whoami
cf-week8-check
test ! -e ~/.ssh/week8_analyst_ed25519 &&   test ! -e ~/.ssh/week8_analyst_ed25519.pub &&   echo "READY: Week 8 key path is unused" ||   echo "STOP: Week 8 key already exists"
```

**Continue only if:** `whoami` prints `analyst`, all checks report `PASS`, and the final line begins with `READY`.

If the final line begins with `STOP`, do not overwrite the key. Ask the instructor whether to resume with the existing key or use the approved reset.

### If the VM Stops

Return to **My Lab Environment** in the Lab Portal and start your assigned VM. A stopped or deallocated VM is not deleted; saved disk files remain.

## Predict First

**[WORKSHEET]** Which file can be distributed when appropriate: the public key or private key? Explain.

```text
The public key file (ending in .pub) can be distributed when appropriate. It is designed to be shared with remote servers or other parties so they can verify your identity or encrypt messages sent to you. Conversely, the private key must never be shared or distributed, as it acts as your secret credentials to prove ownership of the key pair.
```

## Guided Steps

### Step 1 — Prepare the SSH Directory

**[TERMINAL] Run:** analyst@cf-student-07:~$ mkdir -p ~/.ssh analyst@cf-student-07:~$ chmod 700 ~/.ssh

```bash
mkdir -p ~/.ssh
chmod 700 ~/.ssh
```

### Step 2 — Generate the Key Pair

**[TERMINAL] Run:** analyst@cf-student-07:~$ ssh-keygen -t ed25519 -a 100   -f ~/.ssh/week8_analyst_ed25519   -C "week8-analyst-key" Generating public/private ed25519 key pair. Enter passphrase (empty for no passphrase):  Enter same passphrase again:  Your identification has been saved in /home/analyst/.ssh/week8_analyst_ed25519 Your public key has been saved in /home/analyst/.ssh/week8_analyst_ed25519.pub The key fingerprint is: SHA256:6KIKc8hTkHQt4hOZ7WYDIdwf+IemdIEsAh1ACgqA0S8 week8-analyst-key The key's randomart image is: +--[ED25519 256]--+ |#OOo+            | |XO=B +           | |=o*.+ +          | | oE*.* o         | |  =o= o S        | |.... .           | |+o. . .          | |.o.. .           | |...              | +----[SHA256]-----+ analyst@cf-student-07:~$ ^C analyst@cf-student-07:~$

```bash
ssh-keygen -t ed25519 -a 100   -f ~/.ssh/week8_analyst_ed25519   -C "week8-analyst-key"
```

At `Enter passphrase`, create a memorable Week 8 **key passphrase**. Type it again when asked. Nothing may appear while you type; this is normal. Do not use or enter the `analyst` account password unless it happens to be your deliberately chosen key passphrase.

### Step 3 — List the Two Key Files

**[TERMINAL] Run:** analyst@cf-student-07:~$ ls -l ~/.ssh/week8_analyst_ed25519 ~/.ssh/week8_analyst_ed25519.pub -rw------- 1 analyst analyst 464 Sep 19 19:56 /home/analyst/.ssh/week8_analyst_ed25519 -rw-r--r-- 1 analyst analyst  99 Sep 19 19:56 /home/analyst/.ssh/week8_analyst_ed25519.pub

```bash
ls -l ~/.ssh/week8_analyst_ed25519 ~/.ssh/week8_analyst_ed25519.pub
```

**Expected result:** Two filenames appear. The file ending in `.pub` is public. The file without `.pub` is private.

**Evidence moment:** Capture only this listing as `week08-lab03-key-files-permissions.png`.

### Step 4 — Display the Public-Key Fingerprint

**[TERMINAL] Run:** analyst@cf-student-07:~$ ssh-keygen -lf ~/.ssh/week8_analyst_ed25519.pub 256 SHA256:6KIKc8hTkHQt4hOZ7WYDIdwf+IemdIEsAh1ACgqA0S8 week8-analyst-key (ED25519)

```bash
ssh-keygen -lf ~/.ssh/week8_analyst_ed25519.pub
```

**Expected result:** A line containing key size, a `SHA256:` fingerprint, the comment `week8-analyst-key`, and `ED25519`.

**Evidence moment:** Capture the fingerprint as `week08-lab03-public-key-fingerprint.png`.

## Stop & Check

Do not run `cat`, `head`, `tail`, `less`, or `nano` on `~/.ssh/week8_analyst_ed25519`.

### Troubleshooting

- `Saving key ... failed`: confirm you are signed in as `analyst`; do not use `sudo`.
- `No such file` in Step 3 or 4: return to Step 2 and check whether key generation completed.
- Existing-key warning: answer `n` and contact the instructor. Never choose overwrite.

## Explain

**[WORKSHEET]** In 3–4 sentences, explain the handling difference between the two files and the purpose of the key passphrase.

```text
The public key file can be shared freely with remote servers to grant SSH access or verify your identity, whereas the private key file must remain strictly confidential and never be shared, copied, or transmitted. The key passphrase provides an additional layer of security by encrypting the private key file on your local machine. This ensures that even if an unauthorized party gains access to your private key file, they cannot use it without knowing the passphrase to decrypt it.
```

## Analysis Questions

1. Why can the public key be distributed while the private key must remain protected?

```text
The public key is designed specifically for public distribution because it can only be used to encrypt data or verify digital signatures—it cannot be used to decrypt messages or impersonate you.

In contrast, the private key performs the actual decryption and creates the digital signatures that prove your identity. Because public-key cryptography relies on a asymmetric mathematical relationship, anyone with access to your private key can decrypt your confidential messages or sign in to remote servers as if they were you.
```

2. How is the key passphrase different from the `analyst` account password?

```text
The key passphrase is used locally by your SSH client to encrypt and protect your private key file stored on your disk. In contrast, the analyst account password is used by the operating system to authenticate your user session when logging into the system, running administrative tasks, or elevating privileges.
Even if both happen to be identical, they serve entirely different security boundaries: the passphrase protects a specific cryptographic asset on your filesystem, while the account password authenticates your identity to the operating system itself.
```

3. Why did you use a unique Week 8 filename?

```text
I used a unique Week 8 filename (~/.ssh/week8_analyst_ed25519) to avoid accidentally overwriting my default SSH key pairs, such as id_rsa or id_ed25519. Creating a dedicated filename also helps me organize and isolate keys intended for specific labs or projects, making it easier to manage access and revoke specific credentials later without impacting my other SSH connections.
```

## Required Evidence

- `assets/screenshots/week-08/week08-lab03-key-files-permissions.png`
- `assets/screenshots/week-08/week08-lab03-public-key-fingerprint.png`

## Submission Checklist

- [x] The key pair uses the exact Week 8 filenames.

- [x] The private key was never displayed or submitted.

- [x] The fingerprint includes `SHA256:` and `ED25519`.

- [x] Both screenshots use the exact filenames.

- [x] Every worksheet response is complete.

## GitHub / Lab Portal Submission

1. In the Lab Portal, open the matching Week 8 lab.
2. Complete every **[WORKSHEET]** response.
3. Upload only the required screenshots to `assets/screenshots/week-08/`.
4. Select **Submit to GitHub**.
5. Open the committed worksheet and screenshots on GitHub. Confirm they are readable and contain no secrets.

**Never submit:** `.pem` files, files from `~/.ssh/`, passwords, passphrases, private-key contents, or a Bastion shareable URL.
