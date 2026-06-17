# Project Roadmap

## Project

AI Job Opportunity Monitor

---

## Current Status

**Status:** Completed (MVP)

The initial objective of the project was successfully achieved:

- Monitor incoming job-alert emails
- Extract job opportunities automatically
- Classify vacancies using AI
- Score opportunities against predefined criteria
- Deliver structured notifications to Telegram
- Provide direct application links

---

# Phase 0 — Infrastructure Foundation

**Status:** Completed

## Deliverables

- Ubuntu Server deployment
- Docker Engine installation
- Docker Compose installation
- n8n deployment
- Cloudflare Tunnel configuration
- Cloudflare DNS integration
- Domain acquisition and configuration
- SSH key authentication (ED25519)
- UFW firewall configuration
- Automatic service startup
- Infrastructure baseline snapshot
- Remote administration setup

---

# Sprint 1 — Email → AI → Telegram

**Status:** Completed

## Objective

Build an automated pipeline capable of receiving job opportunities from email providers, extracting relevant information, classifying vacancies, and sending structured notifications to Telegram.

## Deliverables

### Email Processing

- [x] IMAP integration
- [x] Email ingestion
- [x] HTML email parsing
- [x] Email normalization
- [x] Sender extraction
- [x] URL extraction

### Job Extraction

- [x] Vacancy detection
- [x] Job title extraction
- [x] Company extraction
- [x] Location extraction
- [x] Application URL extraction
- [x] Multi-platform email support

### AI Processing

- [x] Groq integration
- [x] Llama 3.1 8B Instant integration
- [x] Job opportunity classification
- [x] Structured JSON extraction
- [x] Language detection
- [x] Data validation

### Scoring Engine

- [x] Keyword matching
- [x] Compatibility scoring
- [x] Recommendation generation
- [x] Candidate profile evaluation

### Notifications

- [x] Telegram Bot integration
- [x] Formatted vacancy messages
- [x] Direct application links
- [x] Structured job summaries

---

# Sprint 2 — Persistence Layer

**Status:** Deferred

## Planned Goals

- Database integration
- Vacancy storage
- Duplicate detection
- Historical records
- Searchable job archive
- Vacancy lifecycle tracking

## Possible Technologies

- PostgreSQL
- SQLite
- Supabase

---

# Sprint 3 — Candidate Intelligence

**Status:** Deferred

## Planned Goals

- Resume matching
- Candidate profile scoring
- Language-aware recommendations
- CV selection logic
- Personalized ranking system

---

# Sprint 4 — Application Automation

**Status:** Deferred

## Planned Goals

- Cover letter generation
- Application tracking
- Email drafting
- Automated application workflows
- Application status monitoring

---

# Sprint 5 — Analytics & Reporting

**Status:** Deferred

## Planned Goals

- Vacancy statistics
- Technology trend analysis
- Hiring market analysis
- Skills demand tracking
- Reporting dashboards

---

# Future Enhancements

## Infrastructure

- PostgreSQL migration
- Watchtower deployment
- Automated backups
- Monitoring stack
- CI/CD pipelines
- Infrastructure as Code

## AI

- Multi-model support
- Advanced vacancy ranking
- Salary extraction
- Benefits extraction
- Recruiter identification

## Integrations

- LinkedIn
- Glassdoor
- Indeed
- OCC Mundial
- Computrabajo
- Additional recruitment platforms

---

# MVP Completion Summary

## Infrastructure

- Completed

## Email Processing

- Completed

## AI Classification

- Completed

## Job Extraction

- Completed

## Scoring Engine

- Completed

## Telegram Notifications

- Completed

## Production Deployment

- Completed

## Documentation

- Completed