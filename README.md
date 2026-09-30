# IncidentLens AI

### The Self-Healing On-Call & Post-Mortem Engineer

## Overview

IncidentLens AI is an AI-powered SRE/DevOps assistant designed to use **Hindsight persistent memory** to improve incident response over time.

Instead of treating every production incident as a completely new problem, IncidentLens AI is designed to recall relevant previous incidents, root causes, resolutions, engineering discussions, and post-mortem knowledge.

The goal is to create an incident-response workflow that becomes more useful as operational knowledge accumulates.

## Problem

Production incidents often require engineers to search through previous incident reports, Slack conversations, pull requests, and post-mortems to identify whether a similar problem has occurred before.

A conventional AI assistant may provide technically valid but generic troubleshooting suggestions without knowing what the engineering team previously learned.

IncidentLens AI addresses this knowledge gap through persistent agent memory.

## Core Workflow

**Incoming Incident → Hindsight Recall → Incident Analysis → Actionable Resolution → Hindsight Retain**

1. An incident or production error is received.
2. IncidentLens AI queries Hindsight for relevant historical experiences.
3. Previous root causes, fixes, and engineering decisions are considered.
4. The agent produces an actionable troubleshooting plan.
5. Once the incident is resolved, the new learning can be retained in Hindsight for future incidents.

## Example

### Incoming Incident

`ERROR 500: Database lock timeout in Payment Microservice`

### Without Persistent Memory

A conventional assistant may suggest generic actions such as:

* Check database connections.
* Inspect active locks.
* Review slow queries.
* Check service logs.

### With Incident Memory

IncidentLens AI is designed to recall a previous incident involving the same service where a migration/background worker caused database locking.

The historical resolution can then be used as context for the current investigation.

This creates a shift from:

**“What could be causing this?”**

to:

**“Have we solved something like this before, and what did we learn?”**

## Hindsight Integration

Hindsight acts as the persistent memory layer of IncidentLens AI.

The conceptual interaction is:

```python
memories = hindsight.recall(
    "Database lock timeout in Payment Microservice"
)

# Use recalled operational knowledge
# to generate an incident-response plan.

hindsight.retain(
    "Payment service incident resolved after identifying "
    "the database locking issue and applying the documented fix."
)
```

## Architecture

```text
              Incoming Incident
                     |
                     v
             +---------------+
             | IncidentLens  |
             |     Agent     |
             +---------------+
                     |
                     v
             +---------------+
             |   Hindsight   |
             |     Recall    |
             +---------------+
                     |
                     v
          Historical Incidents
          Root Causes & Fixes
                     |
                     v
             Actionable Plan
                     |
                     v
              Incident Fix
                     |
                     v
             +---------------+
             |   Hindsight   |
             |    Retain     |
             +---------------+
                     |
                     v
             New Operational
                  Memory
```

## Key Capabilities

* Persistent incident memory
* Historical root-cause retrieval
* Reusable resolution knowledge
* Explainable incident-response workflow
* Post-mortem knowledge retention
* Continuous improvement through accumulated operational experience

## Technology Direction

* Python
* Hindsight
* Large Language Model
* FastAPI / Streamlit
* Network and service integrations such as Slack, PagerDuty, GitHub and Kubernetes

## Project Status

This submission presents the IncidentLens AI prototype/concept and its intended Hindsight-powered workflow. Further implementation can extend the system with live integrations, automated incident ingestion, richer post-mortem generation, and production deployment.

## Project Vision

**IncidentLens AI aims to turn incident response from a repeated search for answers into a continuously learning operational workflow.**
