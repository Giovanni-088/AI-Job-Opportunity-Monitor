# Architecture Decision Records (ADR)

## ADR-001 — Use IMAP Instead of Gmail API

**Status:** Accepted

### Decision

Use IMAP as the email ingestion mechanism instead of Gmail-specific integrations.

### Context

The project requires access to the complete email body, including HTML content, in order to accurately extract job information and perform AI-based analysis.

The solution must remain independent from any specific email provider.

### Reason

The workflow requires:

* Full email content retrieval
* HTML parsing
* URL extraction
* Job data extraction
* AI classification and validation

IMAP provides direct access to complete email messages and can be used with different email providers.

### Consequences

#### Pros

* Full email visibility
* Provider-agnostic implementation
* Better extraction accuracy
* Easier migration between email providers

#### Cons

* Requires IMAP configuration
* Requires application passwords or equivalent authentication methods

---

## ADR-002 — Use Cloudflare Tunnel Instead of Port Forwarding

**Status:** Accepted

### Decision

Expose n8n through Cloudflare Tunnel rather than opening ports on the router.

### Context

The platform requires remote access while minimizing infrastructure exposure.

### Reason

Cloudflare Tunnel provides secure access without exposing the origin server directly to the public internet.

### Consequences

#### Pros

* No port forwarding required
* Reduced attack surface
* Automatic HTTPS support
* Simplified remote access
* Additional Cloudflare security controls

#### Cons

* Dependency on Cloudflare services

---

## ADR-003 — Deploy n8n Using Docker

**Status:** Accepted

### Decision

Deploy n8n as a Docker container inside the Ubuntu virtual machine.

### Context

The platform is intended to be portable, reproducible, and easy to maintain.

### Reason

Containerization simplifies deployment, upgrades, backup procedures, and future migrations.

### Consequences

#### Pros

* Reproducible deployments
* Easy upgrades
* Service isolation
* Simplified backup strategy
* Better portability

#### Cons

* Additional Docker layer to manage

---

## ADR-004 — Use a Dedicated Domain

**Status:** Accepted

### Decision

Use a dedicated domain for external access and future integrations.

### Context

The platform requires a stable endpoint for webhooks, remote access, and future services.

### Reason

A dedicated domain improves maintainability and simplifies future expansion.

### Consequences

#### Pros

* Stable endpoint
* Easier integration management
* Improved scalability
* Better separation from infrastructure details

#### Cons

* Domain registration and renewal costs

---

## ADR-005 — Self-Host Infrastructure Inside a Virtual Machine

**Status:** Accepted

### Decision

Run the automation platform inside an Ubuntu Server virtual machine hosted on VMware Workstation.

### Context

The project was designed as a self-hosted learning and production-like environment.

### Reason

Virtualization provides isolation from the host operating system while maintaining flexibility and rollback capabilities.

### Consequences

#### Pros

* Environment isolation
* Snapshot support
* Easier recovery
* Safer experimentation
* Infrastructure portability

#### Cons

* Additional resource consumption compared to bare metal deployment

---

## ADR-006 — Use Groq as the AI Inference Provider

**Status:** Accepted

### Decision

Use Groq-hosted inference instead of running local LLMs.

### Context

The project requires fast and reliable AI inference without maintaining local AI infrastructure.

### Selected Model

```text
llama-3.1-8b-instant
```

### Reason

Groq provides:

* Low latency responses
* Simple API integration
* Reduced infrastructure complexity
* No GPU requirements
* Consistent inference quality

### Consequences

#### Pros

* Fast inference
* No local AI infrastructure
* Reduced maintenance
* Lower hardware requirements
* Easier scalability

#### Cons

* Dependency on external API availability
* Usage-based costs at scale

---

## ADR-007 — Telegram as Notification Channel

**Status:** Accepted

### Decision

Use Telegram as the primary notification channel.

### Context

The platform requires immediate delivery of filtered job opportunities.

### Reason

Telegram provides a simple API, low latency delivery, and rich message formatting capabilities.

### Consequences

#### Pros

* Instant notifications
* Simple integration
* Rich formatting support
* Cross-platform availability

#### Cons

* Dependency on Telegram availability

---

## ADR-008 — AI-Based Validation Before Notification

**Status:** Accepted

### Decision

Validate and enrich extracted job information using an LLM before sending notifications.

### Context

Job platforms use different email formats, making rule-based extraction unreliable in some cases.

### Reason

AI validation improves extraction quality and helps identify:

* Job title
* Company
* Location
* Language
* Job opportunity legitimacy

### Consequences

#### Pros

* Better extraction accuracy
* Platform-independent processing
* Improved data quality

#### Cons

* Additional API calls
* Increased workflow complexity
