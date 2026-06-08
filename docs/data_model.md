# Data Model

## Purpose

This document defines the analytical data model used to investigate the growth slowdown at SynapseOS.

The objective of the data model is not to replicate a production-grade warehouse, but to capture the key business entities, behaviors, and relationships required to diagnose growth, activation, retention, and monetization issues.

The model is intentionally designed around the questions leadership wants answered:

* Which acquisition channels generate the highest-quality customers?
* Where are users dropping off during onboarding?
* What behaviours predict long-term retention?
* Why is free-to-paid conversion declining?
* What is the primary cause of the company's growth slowdown?

---

# Modelling Principles

## Workspace-Centric Design

SynapseOS is a B2B SaaS platform.

The primary customer entity is a workspace rather than an individual user.

This design choice reflects how the business operates:

* Revenue is generated at the workspace level.
* Collaboration occurs at the workspace level.
* Retention is measured at the workspace level.
* The North Star Metric is Weekly Active Workspaces (WAW).

Users are therefore modelled as members of workspaces rather than independent customers.

---

## Event-Driven Analytics

Most business metrics are derived from user and workspace activity.

Instead of storing only aggregated metrics, the model captures key behavioural events that allow us to perform funnel, cohort, retention, and segmentation analyses.

Examples include:

* Integration connected
* Workflow generated
* Automation created
* Report viewed
* Invite sent
* Plan upgraded

This approach enables realistic analytical workflows similar to those used in modern SaaS companies.

---

# Business Entities

The following entities represent the core components of the SynapseOS business.

## Workspace

Represents a customer account.

A workspace is the primary unit of analysis throughout the project.

Examples:

* Startup teams
* Consulting firms
* Product teams

Key business questions:

* Did the workspace activate?
* Is the workspace retained?
* Did the workspace convert to a paid plan?

---

## User

Represents an individual member of a workspace.

Users perform actions that generate events and contribute to workspace success.

Key business questions:

* How do users behave after signing up?
* Which users invite teammates?
* Which users adopt automation features?

---

## Channel

Represents the acquisition source responsible for bringing a user into the product.

Examples:

* Referral
* Product Hunt
* Startup Communities
* LinkedIn Ads
* Google Ads

Key business questions:

* Which channels produce high-quality users?
* Has acquisition quality changed over time?

---

## Integration

Represents a third-party tool connected to SynapseOS.

Examples:

* Gmail
* Slack
* Notion
* Google Drive
* Calendar
* Zoom

Key business questions:

* How many integrations are connected?
* Does integration depth predict retention?

---

## Subscription

Represents a workspace's commercial relationship with the platform.

Key business questions:

* Which workspaces upgrade?
* Which behaviours predict conversion?

---

## Invitation

Represents collaboration growth inside a workspace.

Key business questions:

* Which workspaces invite teammates?
* How does collaboration affect retention and monetization?

---

# Entity Relationships

The analytical model follows the structure below:

```text
Channel
    ↓
User
    ↓
Workspace
    ↓
Events

Workspace
    ↓
Integrations

Workspace
    ↓
Invitations

Workspace
    ↓
Subscriptions
```

Relationship summary:

* One channel can acquire many users.
* One workspace can contain many users.
* One workspace can generate many events.
* One workspace can connect many integrations.
* One workspace can send many invitations.
* One workspace can have subscription history.

---

# Dataset Scale

The simulated company is designed to resemble a seed-to-Series-A stage SaaS startup.

Approximate scale:

| Entity               | Expected Volume |
| -------------------- | --------------: |
| Workspaces           |           8,000 |
| Users                |          25,000 |
| Events               | 300,000-500,000 |
| Invitations          |   20,000-40,000 |
| Subscription Records |          8,000+ |

The scale is intentionally large enough to support meaningful cohort and funnel analyses while remaining manageable in SQL and Excel.

---

# Table Design

## workspaces

Primary business entity.

### Grain

One row per workspace.

### Example Fields

| Column       |
| ------------ |
| workspace_id |
| created_date |
| company_size |
| industry     |
| current_plan |

### Purpose

Provides the foundation for activation, retention, monetization, and segmentation analyses.

---

## users

Workspace members.

### Grain

One row per user.

### Example Fields

| Column       |
| ------------ |
| user_id      |
| workspace_id |
| signup_date  |
| role         |
| channel_id   |

### Purpose

Links acquisition activity to workspace behavior.

---

## channels

Marketing and acquisition sources.

### Grain

One row per acquisition channel.

### Example Fields

| Column       |
| ------------ |
| channel_id   |
| channel_name |
| channel_type |

### Purpose

Supports acquisition quality analysis.

---

## integrations

Available platform integrations.

### Grain

One row per integration.

### Example Fields

| Column           |
| ---------------- |
| integration_id   |
| integration_name |

### Purpose

Defines supported third-party tools.

---

## workspace_integrations

Tracks connected integrations.

### Grain

One row per workspace-integration pair.

### Example Fields

| Column         |
| -------------- |
| workspace_id   |
| integration_id |
| connected_date |

### Purpose

Supports activation and retention analyses.

---

## events

Core behavioural event log.

### Grain

One row per event.

### Example Fields

| Column       |
| ------------ |
| event_id     |
| workspace_id |
| user_id      |
| event_type   |
| event_date   |

### Purpose

Forms the backbone of funnel, cohort, retention, and engagement analyses.

---

## invitations

Collaboration activity.

### Grain

One row per invitation.

### Example Fields

| Column         |
| -------------- |
| invite_id      |
| workspace_id   |
| sender_user_id |
| invite_date    |
| accepted       |

### Purpose

Measures collaboration growth and expansion behaviour.

---

## subscriptions

Commercial activity.

### Grain

One row per subscription period.

### Example Fields

| Column          |
| --------------- |
| subscription_id |
| workspace_id    |
| plan            |
| monthly_revenue |
| start_date      |
| status          |

### Purpose

Supports monetization and revenue analysis.

---

# Event Taxonomy

The following event types are captured within the events table.

## Activation Events

* workspace_created
* integration_connected
* workflow_generated

Used to evaluate onboarding success and activation performance.

---

## Engagement Events

* report_viewed
* automation_created
* task_completed

Used to measure product adoption and value realization.

---

## Collaboration Events

* invite_sent
* invite_accepted

Used to evaluate team expansion and collaboration loops.

---

## Monetization Events

* plan_upgraded
* seat_added

Used to evaluate revenue growth and expansion.

---

## Activity Events

* login
* session_started

Used to measure general product engagement.

---

# Connection to Business Hypotheses

The data model is intentionally designed to test the competing explanations identified in the investigation.

| Hypothesis                   | Primary Tables                 |
| ---------------------------- | ------------------------------ |
| Acquisition Quality Decline  | users, channels                |
| Onboarding Complexity        | events, workspace_integrations |
| Automation Adoption Decline  | events                         |
| Collaboration Loop Weakening | invitations, events            |
| Pricing Friction             | subscriptions                  |
| Market Saturation            | channels, workspaces           |

By mapping business questions directly to entities and tables, the model ensures that every component of the dataset serves a clear analytical purpose.

---

# Design Goal

The purpose of this model is not simply to store data.

It is designed to support a realistic Founder’s Office investigation where growth slowdown emerges from the interaction between acquisition quality, activation, product adoption, collaboration, retention, and monetization.

Every table, event, and relationship exists because it contributes to answering a strategic business question.
