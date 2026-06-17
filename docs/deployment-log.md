# Deployment Log

## Project

**AI Job Opportunity Monitor**

---

## Phase 1 — Windows Deployment

### Objective

Deploy n8n using Docker Desktop and an external SSD.

### Result

Failed

### Root Cause

NTFS permission and volume-mounting issues created instability for persistent n8n storage.

### Decision

Migrate to a Linux-based environment.

---

## Phase 2 — Infrastructure Migration

### Decision

Move deployment to an Ubuntu Server virtual machine.

### Reasons

- Better Docker compatibility
- Native Linux permissions model
- Easier long-term maintenance
- Closer to production environments

### Result

Approved

---

## Phase 3 — Virtual Machine Provisioning

### Platform

VMware Workstation

### Guest Operating System

Ubuntu Server 26.04 LTS

### Result

Success

---

## Phase 4 — Network Configuration

### Initial Goal

Bridged Networking

### Issue

DHCP failed to assign a valid IPv4 address consistently.

### Temporary Solution

NAT Networking

### Result

Success

---

## Phase 5 — SSH Access Configuration

### User Created

```text
n8nserver
```

### Access Method

SSH

### Result

Success

---

## Phase 6 — Security Hardening

### Actions Completed

- Changed default Ubuntu password
- Changed root password
- Installed UFW
- Enabled SSH protection
- Configured n8n authentication

### Result

Success

---

## Phase 7 — UFW Configuration

### Status

Enabled

### Allowed Services

```text
OpenSSH (22/TCP)
```

### Result

Success

---

## Phase 8 — Docker Installation

### Validation

```bash
docker --version
```

### Result

Success

---

## Phase 9 — Docker Compose Verification

### Validation

```bash
docker compose version
```

### Result

Success

---

## Phase 10 — n8n Deployment

### Directory

```text
/opt/n8n
```

### Configuration

- Docker Compose
- Persistent Storage
- Restart Policy: unless-stopped

### Result

Partial Success

### Issue

n8n could not create required configuration files due to permissions.

---

## Phase 11 — Permission Remediation

### Resolution

```bash
chown -R 1000:1000 /opt/n8n/n8n_data
```

### Result

Success

---

## Phase 12 — n8n Validation

### Verification

```bash
docker ps
docker logs n8n
```

### Result

```text
n8n ready on ::, port 5678
```

### Status

Operational

---

## Phase 13 — Temporary Cloudflare Tunnel

### Objective

Expose n8n without router port forwarding.

### Tool

Cloudflared

### Command

```bash
cloudflared tunnel --url http://localhost:5678
```

### Result

Public HTTPS endpoint generated successfully.

### Status

Success

---

## Phase 14 — SSH Key Authentication

### Algorithm

ED25519

### Actions

- Key pair generated
- Public key installed
- Authorized keys configured

### Permissions

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

### Result

Passwordless SSH operational

---

## Phase 15 — Baseline Snapshot

### Objective

Create rollback point before workflow development.

### Actions

- VMware Snapshot created
- n8n data backed up

### Snapshot

```text
PHASE-1-STABLE
```

### Result

Success

---

## Phase 16 — Project Development Started

### Project

AI Job Opportunity Monitor

### Initial MVP

```text
Email
↓
AI Processing
↓
Telegram
```

### Objective

Receive job-related emails, evaluate relevance, and send notifications.

### Status

Development Started

---

## Phase 17 — Domain Acquisition

### Purpose

- Stable public endpoint
- Future integrations
- Cloudflare Tunnel hostname
- Webhook support


### Result

Success

---

## Phase 18 — Cloudflare Migration

### Actions

- DNS migrated to Cloudflare
- Zone activated
- DNS records configured

### Result

Success

---

## Phase 19 — Named Cloudflare Tunnel

### Actions

- Installed cloudflared
- Created named tunnel
- Configured DNS routing
- Installed system service

### Result

Success

## Phase 20 — Public Access Validation

### Test

Incognito browser access

### Result

n8n Sign-In page displayed correctly.

### Status

Operational

---

## Phase 21 — Infrastructure Automation

### Docker

- Automatic restart enabled

### Cloudflared

- Installed as systemd service
- Automatic startup configured

### Validation

Full VM reboot test completed successfully.

### Result

Success

---

## Phase 22 — Email Integration

### Method

IMAP

### Purpose

Retrieve complete email content for AI processing.

### Validation

- Email retrieval successful
- Full HTML content received
- Workflow execution validated

### Result

Operational

---

## Phase 23 — AI Provider Integration

### Provider

Groq

### Model

```text
llama-3.1-8b-instant
```

### Purpose

- Job opportunity detection
- Vacancy extraction
- Company extraction
- Location extraction
- Language detection
- Job validation

### Result

Operational

---

## Phase 24 — Email Normalization Pipeline

### Features Implemented

- HTML cleaning
- URL extraction
- URL normalization
- Source detection
- Email sender normalization
- Job link extraction
- Structured vacancy extraction

### Supported Sources

- Indeed
- Glassdoor
- OCCMundial
- Computrabajo
- LinkedIn
- RemoteOK
- Wellfound

### Result

Operational

---

## Phase 25 — Scoring Engine

### Purpose

Evaluate job relevance according to predefined technologies and keywords.

### Output

- Compatibility score
- Matched keywords
- Recommendation

### Result

Operational

---

## Phase 26 — Telegram Integration

### Features

- Structured notifications
- Direct application URL
- Job title
- Company
- Location
- Score
- Source information

### Result

Operational

---

## Phase 27 — Production Validation

### End-to-End Workflow

```text
Email
↓
IMAP
↓
n8n
↓
HTML Normalization
↓
Job Extraction
↓
Groq AI
↓
Scoring Engine
↓
Telegram
```

### Validation

- Multiple providers tested
- Job extraction verified
- URL extraction verified
- AI classification verified
- Telegram delivery verified

### Result

Success

---

## Final Infrastructure Status

| Component | Status |
|------------|----------|
| Ubuntu Server | Operational |
| VMware Workstation | Operational |
| Docker Engine | Operational |
| Docker Compose | Operational |
| n8n | Operational |
| Cloudflare Tunnel | Operational |
| IMAP Integration | Operational |
| Groq API | Operational |
| Telegram Bot | Operational |
| Job Extraction Engine | Operational |
| Scoring Engine | Operational |

---

## Project Status

### AI Job Opportunity Monitor

```text
Production Ready
```

### Completion Status

```text
Completed
```