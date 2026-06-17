# Troubleshooting

---

# Issue 1 — Docker Volume Permission Error on Windows

## Symptoms

n8n failed to start.

Error:

```text
EACCES: permission denied, open '/home/node/.n8n/config'
```

## Environment

- Windows 10
- Docker Desktop
- External SSD
- NTFS Filesystem

## Investigation

Verified:

- NTFS permissions
- Docker bind mounts
- Container write permissions

Root user could write.

UID 1000 could not write.

## Root Cause

Docker container permissions were incompatible with the mounted NTFS filesystem.

## Resolution

Migration from Windows Docker Desktop to Ubuntu Server VM.

## Status

Resolved

---

# Issue 2 — External SSD Validation

## Symptoms

Windows repeatedly displayed:

```text
Scan and repair drive
```

## Investigation

Commands:

```powershell
Get-PhysicalDisk
wmic diskdrive get model,size,mediatype
```

## Findings

Device detected as:

```text
VendorCo ProductCode USB Device
```

Generic USB enclosure detected.

No filesystem corruption identified.

## Resolution

Drive validation completed.

No action required.

## Status

Resolved

---

# Issue 3 — Ubuntu Installation Media Checksum Failure

## Symptoms

Ubuntu installer reported:

```text
Install media checksum verification failed
```

## Root Cause

Corrupted ISO image.

## Resolution

Downloaded a fresh Ubuntu Server ISO and recreated installation media.

## Status

Resolved

---

# Issue 4 — VMware DHCP Failure

## Symptoms

Ubuntu installer remained indefinitely waiting for DHCP.

No IPv4 address assigned.

Only IPv6 link-local addresses were available.

## Investigation

Commands:

```bash
ip a
ip route
networkctl
```

## Findings

Bridged adapter never received an IPv4 lease.

## Resolution

Switched VM networking mode to NAT.

## Status

Resolved

---

# Issue 5 — SSH Host Key Changed

## Symptoms

```text
WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED
```

## Cause

Original VM was deleted and recreated.

## Resolution

```powershell
ssh-keygen -R <server-ip>
```

Reconnect and accept the new host key.

## Status

Resolved

---

# Issue 6 — Docker Persistence Ownership

## Symptoms

n8n repeatedly crashed during startup.

Error:

```text
EACCES: permission denied, open '/home/node/.n8n/config'
```

## Investigation

```bash
ls -ld /opt/n8n
ls -ld /opt/n8n/n8n_data
```

Output:

```text
root root
```

## Root Cause

Persistence directory ownership was assigned to root.

n8n runs as UID 1000.

## Resolution

```bash
chown -R 1000:1000 /opt/n8n/n8n_data
```

Restart stack:

```bash
docker compose down
docker compose up -d
```

## Status

Resolved

---

# Issue 7 — n8n Startup Validation

## Verification

```bash
docker ps
docker logs n8n
```

Expected:

```text
n8n ready on ::, port 5678
```

## Status

Resolved

---

# Issue 8 — SSH Key Authentication Ignored

## Symptoms

SSH continued requesting a password despite key generation.

## Investigation

```bash
~/.ssh/authorized_keys
```

File existed but was empty.

## Root Cause

Public key was never added to authorized_keys.

## Resolution

Added ED25519 public key.

Applied permissions:

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

## Verification

SSH login completed without password prompt.

## Status

Resolved

---

# Issue 9 — Termius Authentication Failed

## Symptoms

Termius repeatedly requested a password.

## Investigation

SSH logs showed:

```text
Authenticating as "n8n"
```

## Root Cause

Incorrect username configured.

Configured:

```text
n8n
```

Expected:

```text
n8nserver
```

## Resolution

Updated Termius host configuration.

## Verification

Authentication succeeded.

## Status

Resolved

---

# Issue 10 — Cloudflare Tunnel Returning 502 Bad Gateway

## Symptoms

Cloudflare displayed:

```text
502 Bad Gateway
```

## Root Cause

n8n container was stopped.

## Resolution

Started Docker container.

Verification:

```bash
docker ps
```

## Status

Resolved

---

# Issue 11 — Service Validation After Reboot

## Objective

Verify automatic startup after VM reboot.

## Verification

Docker:

```bash
docker ps
```

Expected:

```text
n8n container running
```

Cloudflared:

```bash
systemctl status cloudflared
```

Expected:

```text
active (running)
```

Public Access:

```text
https://n8n.xxxx.xx
```

## Result

All services started automatically.

## Status

Resolved

---

# Issue 12 — Gmail Trigger Limitations

## Symptoms

Gmail Trigger only exposed:

- Subject
- Sender
- Snippet

Missing:

- Full email body
- Complete HTML content

## Impact

AI could not properly analyze vacancies.

## Resolution

Replaced Gmail Trigger with IMAP email ingestion.

## Benefits

- Full email body access
- HTML processing
- Better vacancy extraction
- Platform-independent implementation

## Status

Resolved

---

# Issue 13 — Incorrect Job URL Extraction

## Symptoms

AI frequently returned:

- Tracking links
- Newsletter links
- Unsubscribe links

instead of application URLs.

## Root Cause

LLM attempted to determine URLs directly from email content.

## Resolution

Created dedicated URL normalization workflow.

Features:

- HTML href extraction
- URL filtering
- Source-specific URL selection
- Tracking link removal

## Result

Reliable application URL extraction.

## Status

Resolved

---

# Issue 14 — Incorrect Company Detection

## Symptoms

AI occasionally selected the wrong company from emails containing multiple vacancies.

Example:

```text
Expected:
Webrunner Media Group

Detected:
titiapps
```

## Root Cause

LLM selected a nearby company name from recommendation sections.

## Resolution

Improved extraction pipeline.

Implemented:

- Structured vacancy extraction before AI processing
- Source-specific parsing logic
- Context-aware validation prompts

## Status

Resolved

---

# Issue 15 — Incorrect Job Title Detection

## Symptoms

AI extracted job-alert search terms instead of actual vacancy titles.

Example:

```text
Expected:
IT Business Analyst (Jr/Mid)

Detected:
desarrollador jr
```

## Root Cause

Email subject contained search keywords rather than vacancy titles.

## Resolution

Prompt updated to prioritize:

1. Actual vacancy title
2. Job card title
3. Vacancy heading

and ignore:

- Email subjects
- Search alerts
- Saved search names

## Status

Resolved

---

# Issue 16 — AI JSON Formatting Errors

## Symptoms

LLM occasionally returned:

- Markdown
- Code blocks
- Invalid JSON

## Resolution

Implemented strict JSON-only prompts.

Validation added before workflow continuation.

## Status

Resolved

---

# Issue 17 — Telegram Notification Formatting

## Symptoms

Messages were difficult to read due to inconsistent formatting.

## Resolution

Created standardized Telegram template including:

- Job title
- Company
- Location
- Score
- Recommendation
- Application URL

## Status

Resolved

---

# Operational Verification Commands

## Docker

```bash
docker ps
docker logs n8n
```

## Cloudflared

```bash
systemctl status cloudflared
systemctl restart cloudflared
```

## Network

```bash
ip a
ip route
```

## SSH

```bash
ssh n8nserver@<server-ip>
```

## Firewall

```bash
sudo ufw status
```

## n8n

```bash
docker restart n8n
```

---

# Current Known Issues

No active issues identified.

System operating normally.