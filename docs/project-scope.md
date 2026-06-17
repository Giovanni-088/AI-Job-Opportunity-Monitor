# AI Job Opportunity Monitor

## Project Overview

AI Job Opportunity Monitor is a self-hosted automation system designed to automatically monitor incoming job-alert emails, extract relevant vacancy information, evaluate opportunities against predefined criteria, and deliver structured notifications directly to Telegram.

The platform focuses on reducing manual job searching by filtering and prioritizing opportunities that align with the target professional profile.

---

## Objective

Automatically discover, analyze, score, and notify relevant job opportunities from multiple recruitment platforms.

---

## Target Profiles

The scoring system is optimized for roles related to:

- DevOps Engineer
- Automation Engineer
- Integration Engineer
- Platform Engineer
- Site Reliability Engineer (SRE)
- Cloud Engineer
- Infrastructure Engineer
- AI Automation Specialist

---

## Supported Job Sources

Current sources:

- Indeed
- Glassdoor
- Computrabajo
- OCC Mundial
- LinkedIn
- Remote Ok
- Wellfound

Future sources:

- Additional recruitment platforms

---

## Core Features

### Email Processing

- IMAP email ingestion
- HTML email parsing
- Text normalization
- Sender identification
- Application URL extraction

### Job Extraction

- Job title extraction
- Company extraction
- Location extraction
- Application URL extraction
- Language detection

### AI Analysis

- Job opportunity validation
- Structured information extraction
- Vacancy classification
- Relevance scoring
- Candidate profile matching

### Notification System

- Telegram integration
- Structured vacancy notifications
- Direct application links
- Compatibility score display

---

## Notification Channel

### Telegram

Purpose:

- Real-time job alerts
- Structured vacancy delivery
- Direct access to application links

---

## Workflow Engine

### n8n

Responsibilities:

- Email ingestion
- Workflow orchestration
- AI integration
- Data processing
- Notification delivery

---

## AI Engine

### Provider

Groq

### Model

```text
llama-3.1-8b-instant
```

Responsibilities:

- Vacancy validation
- Information extraction
- Language detection
- Data correction
- Job classification

---

## Infrastructure

### Operating System

```text
Ubuntu Server 26.04 LTS
```

### Container Platform

```text
Docker
Docker Compose
```

### Remote Access

```text
Cloudflare Tunnel
```

### Hosting Environment

```text
Windows 10
VMware Workstation
Ubuntu Server VM
```

---

## Data Flow

```text
Recruitment Platforms
          │
          ▼
      Email Inbox
          │
          ▼
          IMAP
          │
          ▼
          n8n
          │
          ▼
      AI Analysis
          │
          ▼
   Scoring Engine
          │
          ▼
 Telegram Notification
```

---

## Scoring System

The platform evaluates vacancies using predefined criteria, including:

- Relevant technologies
- Required skills
- Job title relevance
- Remote work availability
- Professional profile alignment

Output:

- Compatibility Score
- Recommendation Level
- Matched Keywords

---

## Current Status

### Project Stage

**MVP Completed**

### Completed Features

- Infrastructure deployment
- IMAP integration
- Email parsing
- Vacancy extraction
- AI classification
- Relevance scoring
- Telegram notifications
- Multi-platform support
- Direct application links

### Current Activity

- Documentation finalization
- Repository organization
- Project publication

---

## Future Enhancements

### Persistence Layer

- PostgreSQL integration
- Vacancy history
- Duplicate detection

### Candidate Intelligence

- Resume matching
- Personalized recommendations
- Cover letter generation

### Analytics

- Market trend analysis
- Technology demand tracking
- Vacancy reporting dashboards

### Automation

- Application tracking
- Automated application workflows
- Recruiter identification