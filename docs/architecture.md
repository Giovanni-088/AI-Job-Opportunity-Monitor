# Architecture

## Project

**AI Job Opportunity Monitor**

---

## Overview

AI Job Opportunity Monitor is a self-hosted automation platform designed to automatically monitor, classify, score, and notify job opportunities received from multiple recruitment platforms via email.

The system processes incoming job-alert emails, extracts structured job data, evaluates relevance according to predefined criteria, and delivers filtered opportunities directly to Telegram.

The platform is designed to be lightweight, modular, self-hosted, and easily extensible for future automation projects.

---

## Infrastructure

### Host Machine

* Windows 10

### Hypervisor

* VMware Workstation

### Virtual Machine

* Ubuntu Server 26.04 LTS

### Container Runtime

* Docker Engine
* Docker Compose

---

## Current Infrastructure Architecture

```text
Windows 10 Host

└── VMware Workstation
    └── Ubuntu Server 26.04 LTS
        ├── Docker Engine
        ├── Docker Compose
        ├── n8n
        └── Cloudflared
```

---

## External Services

```text
Gmail (IMAP)
Telegram Bot API
Cloudflare Tunnel
Groq API
```

---

## Network Architecture

### Internal Network

Current mode:

* NAT

Internal VM IP:

* Private LAN Address

### Future Improvements

* Bridged Network
* Static IP Assignment

---

## Container Platform

### Docker Engine

Purpose:

* Service isolation
* Environment consistency
* Simplified deployment
* Portability

### Docker Compose

Purpose:

* Service orchestration
* Configuration management
* Infrastructure reproducibility

---

## Services

### n8n

Container Image:

```
docker.n8n.io/n8nio/n8n
```

Port:

```
5678
```

Persistence:

```
/opt/n8n/n8n_data
```

Restart Policy:

```
unless-stopped
```

Purpose:

* Workflow orchestration
* Email ingestion
* AI integration
* Telegram notifications

---

### Cloudflared

Purpose:

* Secure remote access
* Tunnel-based connectivity
* Elimination of public port exposure

---

### Groq

Provider:

* Groq

Model:

```
llama-3.1-8b-instant
```

Purpose:

* LLM inference
* Job classification
* Structured data extraction
* Job validation

---

## Data Flow

```text
Job Platform Email
        │
        ▼
 Gmail (IMAP)
        │
        ▼
 n8n Workflow
        │
        ├── Email Parsing
        │
        ├── URL Extraction
        │
        ├── Job Extraction
        │
        ├── AI Classification
        │
        ├── Relevance Scoring
        │
        └── Telegram Formatting
        │
        ▼
 Telegram Notification
```

---

## AI Processing Pipeline

```text
Email
  │
  ▼
HTML Extraction
  │
  ▼
Text Normalization
  │
  ▼
Job Detection
  │
  ▼
Structured Extraction
  │
  ▼
AI Validation
  │
  ▼
Scoring Engine
  │
  ▼
Telegram Delivery
```

---

## Directory Structure

```
/opt
└── n8n
    ├── docker-compose.yml
    └── n8n_data
```

Planned Structure:

```
/opt
├── n8n
├── cloudflared
├── backups
├── scripts
├── monitoring
└── docs
```

---

## Administration

### Access Methods

* SSH
* SSH ED25519 Key Authentication
* Termius
* PowerShell

### Administrative Users

Standard User:

```
n8nserver
```

Administrative User:

```
root
```

---

## Security Controls

### Network Security

* Cloudflare Tunnel
* No public port forwarding
* Private NAT network
* No public AI endpoints exposed

### Host Security

* UFW Firewall Enabled
* SSH Key Authentication
* Docker Service Isolation

### Application Security

* n8n Authentication
* Cloudflare Protected Endpoint

---

## External Access Architecture

```
Internet
    │
    ▼
Cloudflare
    │
    ▼
Cloudflare Tunnel
    │
    ▼
n8n
    │
    ▼
Docker
    │
    ▼
Ubuntu VM
    │
    ▼
VMware Workstation
    │
    ▼
Windows Host
```

---

## Exposed Services

### SSH

```
TCP/22
```

### n8n

```
TCP/5678
```

Accessible only through Cloudflare Tunnel.

---

## Design Decisions

### Ubuntu Server

Reasons:

* Low resource consumption
* Docker-native environment
* Stable server platform
* Production-oriented architecture

### Docker

Reasons:

* Service isolation
* Portability
* Reproducibility
* Simplified maintenance

### VMware Workstation

Reasons:

* Snapshot support
* Easy rollback capability
* Stable virtualization environment

### Cloudflare Tunnel

Reasons:

* No exposed public ports
* Simplified remote access
* Additional security layer

### AI Provider Selection

Reasons:

* Low latency inference
* Simple API integration
* Reduced infrastructure complexity
* No local GPU requirements
* Cost-effective for low-volume workloads

```
```
