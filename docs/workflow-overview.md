# Workflow Overview

## Purpose

AI Job Opportunity Monitor automatically discovers, validates, scores, and notifies relevant job opportunities received through recruitment emails.

The workflow eliminates manual review of job-alert emails by extracting structured vacancy information, evaluating relevance through artificial intelligence, and delivering curated opportunities directly to Telegram.

---

# High-Level Workflow

```text
Email Provider
      │
      ▼
IMAP Email Trigger
      │
      ▼
Email Processing
      │
      ▼
HTML Parsing & Cleanup
      │
      ▼
Source Detection
      │
      ▼
Vacancy Extraction
      │
      ▼
URL Normalization
      │
      ▼
AI Validation
      │
      ▼
Compatibility Scoring
      │
      ▼
Notification Formatting
      │
      ▼
Telegram Delivery
```

---

# Detailed Workflow

## 1. Email Ingestion

### Component

IMAP Trigger

### Purpose

Continuously monitor the mailbox for incoming job-alert emails.

### Input

Emails received from:

* Indeed
* Glassdoor
* Computrabajo
* LinkedIn
* OCC Mundial
* Other recruitment platforms

### Output

Raw email data:

* Subject
* Sender
* Date
* HTML body

---

## 2. Email Processing

### Purpose

Prepare email content for downstream processing.

### Operations

* HTML extraction
* Text cleanup
* Character normalization
* Encoding correction

### Output

Clean text representation of the original email.

---

## 3. Source Detection

### Purpose

Identify the recruitment platform that generated the email.

### Supported Sources

- Indeed
- Glassdoor
- OCCMundial
- Computrabajo
- LinkedIn
- RemoteOK
- Wellfound

### Output

Source identifier used by extraction logic.

Example:

```json
{
  "source": "glassdoor"
}
```

---

## 4. Vacancy Extraction

### Purpose

Extract structured vacancy information from the email content.

### Extracted Fields

* Job Title
* Company
* Location
* Application URL
* Email Metadata

### Platform-Specific Logic

Custom extraction rules are applied depending on the detected source.

### Output

Structured vacancy object.

Example:

```json
{
  "job_title": "Integrations/Automation Specialist",
  "company": "Webrunner Media Group",
  "location": "Remote"
}
```

---

## 5. URL Normalization

### Purpose

Identify the actual vacancy URL and eliminate irrelevant links.

### Removes

* Tracking URLs
* Marketing URLs
* Unsubscribe links
* Privacy policy links
* Social media links
* Analytics redirects

### Output

Single validated application URL.

Example:

```json
{
  "applyUrl": "https://job-platform.com/job/123"
}
```

---

## 6. AI Validation

### Provider

Groq

### Model

```text
llama-3.1-8b-instant
```

### Purpose

Validate and correct extracted information.

### Responsibilities

* Job title verification
* Company verification
* Location verification
* Language detection
* Vacancy validation
* Structured JSON generation

### Output

Validated vacancy object.

---

## 7. Compatibility Scoring

### Purpose

Measure how well the opportunity aligns with predefined career goals.

### Evaluation Criteria

* DevOps relevance
* Automation relevance
* Integration relevance
* Platform Engineering relevance
* Remote availability
* Technology stack compatibility

### Output

Score and recommendation.

Example:

```json
{
  "score": 85,
  "recommendation": "APPLY"
}
```

---

## 8. Notification Generation

### Purpose

Create a human-readable summary of the opportunity.

### Included Information

* Job Title
* Company
* Location
* Score
* Recommendation
* Direct Application URL

### Output

Telegram-ready message.

---

## 9. Telegram Delivery

### Purpose

Notify the user of relevant opportunities.

### Channel

Telegram Bot API

### Final Output

Real-time notification containing:

* Vacancy information
* Compatibility score
* Direct application link

---

# Data Flow Diagram

```text
Recruitment Platforms
        │
        ▼
 IMAP Inbox
        │
        ▼
 Email Trigger
        │
        ▼
 HTML Processing
        │
        ▼
 Source Detection
        │
        ▼
 Vacancy Extraction
        │
        ▼
 URL Normalization
        │
        ▼
 Groq AI Validation
        │
        ▼
 Scoring Engine
        │
        ▼
 Telegram Formatter
        │
        ▼
 Telegram Notification
```

---

# Workflow Outputs

The workflow produces a structured vacancy object containing:

```json
{
  "job_title": "",
  "company": "",
  "location": "",
  "application_url": "",
  "score": 0,
  "recommendation": "",
  "matchedKeywords": []
}
```

---

# Current Status

```text
Production Ready
```

The workflow has been fully implemented, tested, and validated for operational use.
