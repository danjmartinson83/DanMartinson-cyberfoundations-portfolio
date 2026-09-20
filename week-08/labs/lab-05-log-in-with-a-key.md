# Week 8 Lab 05 — Log In with a Key

**Student Name:** Dan Martinson

**Date Completed:** 9/19/2026

**Module:** 3 — Practical Cryptography  
**Submission Path:** `week-08/labs/lab-05-log-in-with-a-key.md`

> ## STOP — Protect secrets
> Never paste, upload, commit, or screenshot a password, passphrase, or private key. Do not run `cat` on any private-key file. Submit only the worksheet and the named screenshots. Keep all cryptographic files on the VM.

## How to Use This Lab

- **[TERMINAL]** means type or paste the command into the Cloud Heights terminal.
- **[WORKSHEET]** means type your response in this lab worksheet.
- Run commands in the order shown. Do not type the sample output.
- If your result does not match the stated success check, stop at the Troubleshooting box. Do not improvise with `sudo`, package installation, Azure settings, or SSH server configuration.

## Mission

Authorize the public key created in Lab 03 and prove that `analyst@localhost` authenticates with that key without falling back to the account password.

## What You Already Know

In Week 6, SSH used the `analyst` account password. Here, the server stores the public key in `authorized_keys`, while the private key stays in the client account. The same user, protocol, and destination remain; only the authentication method changes.

## Lab Environment / Pre-Lab Check

**Required prerequisite:** Complete Lab 03 first.

**[TERMINAL] Run:** whoami cf-week8-check test -f ~/.ssh/week8_analyst_ed25519 &&   test -f ~/.ssh/week8_analyst_ed25519.pub &&   echo "READY: Lab 03 key pair exists" ||   echo "STOP: complete Lab 03 before continuing"

```bash
whoami
cf-week8-check
test -f ~/.ssh/week8_analyst_ed25519 &&   test -f ~/.ssh/week8_analyst_ed25519.pub &&   echo "READY: Lab 03 key pair exists" ||   echo "STOP: complete Lab 03 before continuing"
```

**Continue only if:** `whoami` prints `analyst`, all checks report `PASS`, and the final line begins with `READY`.

### If the VM Stops

Return to **My Lab Environment** in the Lab Portal and start your assigned VM. A stopped or deallocated VM is not deleted; saved disk files remain.

## Predict First

**[WORKSHEET]** Does the private key need to be copied into `authorized_keys`? Explain.

```text
No, the private key should never be copied into authorized_keys.

The authorized_keys file resides on the destination server and only stores public keys, which act like a lock allowing access to anyone holding the corresponding key. The private key acts as the secret personal key and must remain securely on the client machine to prove your identity. Copying the private key to the server or exposing it in authorized_keys compromises security and defeats the purpose of asymmetric key authentication.
```

## Guided Steps

### Step 1 — Prepare `authorized_keys`

**[TERMINAL] Run:** mkdir -p ~/.ssh , chmod 700 ~/.ssh , touch ~/.ssh/authorized_keys,

```bash
mkdir -p ~/.ssh
chmod 700 ~/.ssh
touch ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
```

### Step 2 — Add the Week 8 Public Key Once

**[TERMINAL] Run:** grep -qxF "$(cat ~/.ssh/week8_analyst_ed25519.pub)" ~/.ssh/authorized_keys   || cat ~/.ssh/week8_analyst_ed25519.pub >> ~/.ssh/authorized_keys

```bash
grep -qxF "$(cat ~/.ssh/week8_analyst_ed25519.pub)" ~/.ssh/authorized_keys   || cat ~/.ssh/week8_analyst_ed25519.pub >> ~/.ssh/authorized_keys
```

This command adds the key only if an identical line is not already present.

### Step 3 — Confirm the Entry and Safe Permissions

**[TERMINAL] Run:** grep -c 'week8-analyst-key$' ~/.ssh/authorized_keys  ,  stat -c '%a %n' ~/.ssh ~/.ssh/authorized_keys

```bash
grep -c 'week8-analyst-key$' ~/.ssh/authorized_keys
stat -c '%a %n' ~/.ssh ~/.ssh/authorized_keys
```

**Required result:** The count is `1`; permissions show `700` for `.ssh` and `600` for `authorized_keys`.

**Evidence moment:** Capture this result as `week08-lab05-authorized-key-permissions.png`.

### Step 4 — Run the Public-Key-Only Proof

**[TERMINAL] Run:** ssh   -o PreferredAuthentications=publickey   -o PasswordAuthentication=no   -i ~/.ssh/week8_analyst_ed25519   analyst@localhost   'echo "AUTH_TEST=PUBLICKEY_SUCCESS"; whoami; hostname'

```bash
ssh   -o PreferredAuthentications=publickey   -o PasswordAuthentication=no   -i ~/.ssh/week8_analyst_ed25519   analyst@localhost   'echo "AUTH_TEST=PUBLICKEY_SUCCESS"; whoami; hostname'
```

If SSH asks whether to trust the host fingerprint, type `yes` and press Enter. If no fingerprint question appears, continue; `localhost` was already known. Do not delete `known_hosts` to force the question.

At `Enter passphrase for key`, enter the **Lab 03 key passphrase**. Do not enter the `analyst` account password.

**Required result:** AUTH_TEST=PUBLICKEY_SUCCESS analyst cf-student-07

```text
AUTH_TEST=PUBLICKEY_SUCCESS
analyst
cf-student-XX
```

The final hostname will contain your assigned VM number instead of `XX`.

**Evidence moment:** Capture the three result lines as `week08-lab05-publickey-auth-success.png`.

## Stop & Check

If the command asks for the `analyst` account password, reports `Permission denied`, or does not print `AUTH_TEST=PUBLICKEY_SUCCESS`, do not submit. The options in the proof command disable account-password fallback for this one test only; they do not change the VM server.

### Troubleshooting

1. Run `grep -c 'week8-analyst-key$' ~/.ssh/authorized_keys`; required value is `1`.
2. Run `stat -c '%a %n' ~/.ssh ~/.ssh/authorized_keys`; required values are `700` and `600`.
3. Run `ssh-keygen -lf ~/.ssh/week8_analyst_ed25519.pub`; it must show the Lab 03 key.
4. If any check fails, stop and contact the instructor. Do not edit `/etc/ssh/sshd_config`, use `sudo`, disable password authentication, or delete `known_hosts`.

## Explain

**[WORKSHEET]** In 4–5 sentences, compare Week 6 password authentication with this key-based test. State what changed and what stayed the same.

```text
In both tests, the target SSH user (analyst), destination host (localhost), and underlying SSH protocol remained identical. What changed was the authentication mechanism used to verify the user's identity. In Week 6, access relied on authenticating with the analyst account password directly. In contrast, this test used asymmetric cryptography, where the server validated access by matching the client's private key against the public key placed in authorized_keys. Consequently, password fallback was explicitly disabled during this test, relying solely on key-based verification.
```

## Analysis Questions

1. What changed between the Week 6 and Week 8 SSH logins?

```text
Between the Week 6 and Week 8 SSH logins, the primary change was the authentication mechanism:
Authentication Method: Week 6 used standard account password authentication, whereas Week 8 used asymmetric key-based authentication (ed25519 key pair).
Credential Used: Week 6 required entering the analyst user account password. Week 8 relied on a private key stored on the client machine verified against a public key placed in ~/.ssh/authorized_keys (and protected by a key passphrase).
Password Fallback: In Week 8, password authentication fallback was explicitly disabled during the test command (-o PasswordAuthentication=no), requiring access strictly via the public key.
```

2. What stayed the same?

```text
The following elements remained identical between the Week 6 and Week 8 SSH logins:
Target User Account: You authenticated as the analyst user in both tests.
Destination Host: The SSH connection target was localhost (the local virtual machine).
Network Port and Protocol: Both connections used the standard SSH protocol operating over TCP port 22.
Underlying SSH Architecture: The basic client-server relationship and shell environment accessed upon successful login remained the same.
```

3. Why does `authorized_keys` contain the public key rather than the private key?

```text
The authorized_keys file contains the public key because of how asymmetric cryptography works:
Public Keys are Open: A public key acts like a lock. It is designed to be shared openly and placed on destination servers in authorized_keys so the server knows which identities are permitted to log in.
Private Keys are Secret: A private key acts like the unique physical key. It must stay securely on the client machine and never be shared or copied to a remote server.
During authentication, the server uses the public key in authorized_keys to generate a cryptographic challenge that can only be solved by someone holding the matching private key, proving identity without ever exposing the secret key itself.
```

4. Why is the forced proof stronger evidence than a normal successful SSH login?

```text
The forced proof is stronger evidence because it explicitly forces SSH to use key-based authentication while blocking password authentication (-o PasswordAuthentication=no).
In a normal SSH login, the client and server negotiate authentication methods automatically. If public key authentication fails—for example, due to incorrect key permissions or a missing public key—SSH may silently fall back to prompting for the account password. A successful login under normal conditions doesn't definitively prove that public key authentication worked.
By disabling password fallback and restricting authentication solely to the public key (-o PreferredAuthentications=publickey), the test guarantees that a successful connection could only have been achieved using the SSH key pair, conclusively verifying that the key setup and permissions are correct.
```

5. How is the key passphrase different from the `analyst` account password?

```text
The key passphrase and the analyst account password serve two fundamentally different security functions:
What it protects: The key passphrase encrypts and protects the private key file locally on your client machine. In contrast, the analyst account password protects the system account and user session on the remote server.
Where it is evaluated: The key passphrase is processed entirely on your local machine by the local SSH agent/client to unlock the private key for use. The account password, however, is sent to (and validated by) the remote server's authentication system (PAM/sshd).
Cryptographic role: The key passphrase acts as a local protection layer so that if your private key file is stolen or leaked, an attacker still cannot use it without knowing the passphrase. The account password directly grants access to the server's user account itself.
```

## Required Evidence

- `assets/screenshots/week-08/week08-lab05-authorized-key-permissions.png`
- `assets/screenshots/week-08/week08-lab05-publickey-auth-success.png`

## Submission Checklist

- [x] Lab 03 was completed first.

- [x] The authorized-key count is exactly `1`.

- [x] Permissions are `700` and `600`.

- [x] The public-key-only proof printed all three required lines.

- [x] Both screenshots use the exact filenames.

- [x] No password, passphrase, private key, or Bastion URL appears.

- [x] Every worksheet response is complete.

## GitHub / Lab Portal Submission

1. In the Lab Portal, open the matching Week 8 lab.
2. Complete every **[WORKSHEET]** response.
3. Upload only the required screenshots to `assets/screenshots/week-08/`.
4. Select **Submit to GitHub**.
5. Open the committed worksheet and screenshots on GitHub. Confirm they are readable and contain no secrets.

**Never submit:** `.pem` files, files from `~/.ssh/`, passwords, passphrases, private-key contents, or a Bastion shareable URL.
