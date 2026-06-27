# AI Job Opportunity Monitor

## Executive Summary

AI Job Opportunity Monitor is a self-hosted intelligent automation platform designed to continuously monitor, process, evaluate, and prioritize job opportunities received through email-based recruitment channels.

The platform automates the complete job discovery workflow, transforming unstructured recruitment emails into actionable opportunities through a combination of workflow orchestration, artificial intelligence, rule-based evaluation, and real-time notification delivery.

The primary objective of the project is to reduce the time and effort required to identify relevant career opportunities while increasing the probability of discovering positions aligned with predefined professional goals.

This project was developed as a practical implementation of modern Automation Engineering, AI Integration, Infrastructure Management, and Workflow Orchestration principles.

---

# Business Problem

Professionals actively seeking career opportunities often receive large volumes of recruitment emails from multiple job platforms.

These emails typically contain:

* Mixed content
* Marketing material
* Multiple job recommendations
* Tracking links
* Inconsistent formatting
* Platform-specific structures

Manually reviewing these notifications introduces several challenges:

* Significant time consumption
* High probability of overlooking relevant opportunities
* Difficulty prioritizing vacancies
* Lack of centralized evaluation criteria

AI Job Opportunity Monitor addresses these challenges by automatically identifying, extracting, validating, scoring, and notifying relevant job opportunities.

---

# Solution Overview

The platform operates as an event-driven automation system.

Incoming job-alert emails are automatically processed through a multi-stage pipeline that performs:

1. Email ingestion
2. HTML parsing
3. Content normalization
4. Vacancy extraction
5. URL normalization
6. AI-assisted validation
7. Compatibility scoring
8. Telegram notification delivery

The result is a curated stream of opportunities ranked according to predefined professional interests.

---

# Key Features

## Email Monitoring

* Continuous IMAP monitoring
* Multi-platform compatibility
* Automated processing pipeline
* Near real-time execution

Supported platforms include:

* Indeed
* Glassdoor
* Computrabajo
* LinkedIn
* OCC Mundial
* Remote OK
* Wellfound
* Additional providers through generic parsing logic

---

## Vacancy Extraction Engine

The platform analyzes incoming HTML emails and extracts:

* Job Title
* Company Name
* Location
* Application URL
* Job Description
* Required Technologies
* Required Skills

The extraction layer includes custom logic for platform-specific email formats.

---

## URL Normalization Engine

Recruitment platforms frequently use:

* Tracking URLs
* Redirect links
* Marketing parameters
* Analytics URLs

The normalization engine automatically identifies and extracts the real vacancy URL to ensure users are directed to the correct application page.

---

## Artificial Intelligence Layer

The platform leverages Large Language Models through the Groq API.

Current model:

```text
llama-3.1-8b-instant
```

AI responsibilities include:

* Vacancy validation
* Data correction
* Company verification
* Job title verification
* Language detection
* Structured JSON generation

---

## Compatibility Scoring Engine

Each vacancy is evaluated against predefined professional preferences.

The scoring engine considers:

* Technical stack alignment
* Automation relevance
* DevOps relevance
* Remote work availability
* Integration technologies
* Infrastructure technologies

The final score helps prioritize opportunities before notification delivery.

---

## Telegram Notification System

Validated opportunities are delivered directly through Telegram.

Notifications contain:

* Job Title
* Company
* Location
* Score
* Recommendation
* Direct Application URL

This provides immediate access to opportunities without requiring manual email review.

---

# System Architecture

```text
Job Platforms
      │
      ▼
 IMAP Email Inbox
      │
      ▼
      n8n
      │
      ├── Email Parsing
      ├── HTML Normalization
      ├── URL Extraction
      ├── Vacancy Extraction
      ├── AI Validation
      ├── Scoring Engine
      └── Notification Builder
      │
      ▼
 Telegram Delivery Notification
```

---

# Technology Stack

## Infrastructure

* Ubuntu Server 26.04 LTS
* VMware Workstation
* Docker Engine
* Docker Compose
* Cloudflare Tunnel

## Workflow Automation

* n8n

## Artificial Intelligence

* Groq API
* llama-3.1-8b-instant

## Messaging

* Telegram Bot API

## Email Processing

* IMAP

---

# Infrastructure Design

The platform follows a self-hosted architecture designed to maximize control, portability, and cost efficiency.

```text
Windows Host
    │
VMware Workstation
    │
Ubuntu Server
    │
Docker
    │
n8n
    │
Cloudflare Tunnel
```

This design eliminates dependency on expensive SaaS automation platforms while maintaining flexibility and scalability.

---

# Security

Security controls implemented include:

* Cloudflare Tunnel
* No public port forwarding
* SSH key authentication
* UFW firewall
* Docker container isolation
* Cloudflare DNS protection
* Application-level authentication

---

# Project Outcomes

The project successfully demonstrates:

* Workflow orchestration
* Infrastructure deployment
* AI integration
* Email processing
* API integrations
* Self-hosted automation
* Production-ready deployment practices

---

# Future Roadmap

Planned enhancements include:

* PostgreSQL persistence layer
* Historical vacancy analytics
* Multi-user support
* Resume matching engine
* Automated application workflows
* Reporting dashboard
* Infrastructure as Code
* CI/CD pipeline integration
* Additional AI agents

---

# Current Status

```text
Production Ready
```

Core functionality has been fully implemented and validated in a self-hosted environment.

---

# Author

Personal Automation & Integration Engineering Project

Focused on practical applications of:

* DevOps
* Workflow Automation
* Artificial Intelligence
* Infrastructure Engineering

The workflow can be imported directly into n8n from:

workflows/ai-job-opportunity-monitor.json
* Systems Integration

