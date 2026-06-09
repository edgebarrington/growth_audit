# Warehouse Blueprint

## Purpose

This document defines the analytical warehouse used to simulate SynapseOS, an AI-powered work operating system experiencing a growth slowdown.

The warehouse is designed to support a Founder’s Office investigation into the root causes of declining activation, retention, collaboration, conversion, and growth.

The objective is not to create random synthetic data. It is to create realistic business behaviour that enables competing hypotheses to emerge and be tested through analysis.

---

# Design Principles

## Workspace-Centric

The workspace is the primary business entity.

All major business outcomes are measured at the workspace level:

* Activation
* Engagement
* Retention
* Conversion
* Revenue

This aligns with the company's North Star Metric:

**Weekly Active Workspaces (WAW)**

---

## Event-Driven

Behaviour is represented through events rather than pre-aggregated metrics.

This enables:

* Funnel analysis
* Cohort analysis
* Retention analysis
* Segmentation
* Growth decomposition

Most KPIs will be derived from the events table.

---

## Hypothesis-Driven

The warehouse must support evaluation of six competing explanations:

* H1 Acquisition Quality Decline
* H2 Onboarding Complexity
* H3 Automation Adoption Decline
* H4 Collaboration Loop Weakening
* H5 Pricing Friction
* H6 Market Saturation

No table should exist unless it contributes to testing one or more hypotheses.

---

# Warehouse Overview

```text
channels
    ↓
users
    ↓
workspaces
    ↓
events

workspaces
    ↓
workspace_integrations

workspaces
    ↓
invitations

workspaces
    ↓
subscriptions
```

---

# Table Specifications

## workspaces

### Grain

One row per workspace.

### Estimated Volume

~8,000 rows

### Purpose

Primary customer entity.

Supports:

* Acquisition analysis
* Activation analysis
* Retention analysis
* Monetization analysis

### Key Fields

| Column                 | Description                    |
| ---------------------- | ------------------------------ |
| workspace_id           | Unique workspace identifier    |
| created_date           | Workspace creation date        |
| acquisition_channel_id | Original acquisition source    |
| company_size           | Startup size segment           |
| industry               | Industry classification        |
| current_plan           | Free / Pro / Team / Enterprise |
| workspace_status       | Active / Churned               |

### Business Logic

Every workspace enters through an acquisition channel and serves as the primary unit for all KPI calculations.

---

## users

### Grain

One row per user.

### Estimated Volume

~25,000 rows

### Purpose

Represents members of workspaces.

Supports:

* Collaboration analysis
* Team growth analysis
* User segmentation

### Key Fields

| Column                 | Description                 |
| ---------------------- | --------------------------- |
| user_id                | Unique user identifier      |
| workspace_id           | Associated workspace        |
| signup_date            | User join date              |
| role                   | Founder, Manager, IC, Admin |
| acquisition_channel_id | Original acquisition source |

### Business Logic

Users inherit workspace behaviour but generate individual activity events.

---

## channels

### Grain

One row per acquisition source.

### Estimated Volume

5-8 rows

### Example Values

* Referral
* Product Hunt
* Startup Communities
* LinkedIn Ads
* Google Ads

### Purpose

Supports acquisition quality analysis.

### Key Fields

| Column       | Description             |
| ------------ | ----------------------- |
| channel_id   | Unique identifier       |
| channel_name | Channel name            |
| channel_type | Organic, Referral, Paid |

### Business Logic

Channels have different activation and retention characteristics.

Referral users should exhibit the strongest downstream performance.

---

## integrations

### Grain

One row per integration.

### Estimated Volume

5-10 rows

### Example Values

* Gmail
* Slack
* Notion
* Google Drive
* Calendar
* Zoom

### Purpose

Defines available ecosystem integrations.

### Key Fields

| Column           | Description       |
| ---------------- | ----------------- |
| integration_id   | Unique identifier |
| integration_name | Integration name  |

---

## workspace_integrations

### Grain

One row per workspace-integration relationship.

### Estimated Volume

20,000-30,000 rows

### Purpose

Measures adoption depth.

Supports:

* Activation analysis
* Retention analysis
* Value realization analysis

### Key Fields

| Column         | Description           |
| -------------- | --------------------- |
| workspace_id   | Workspace             |
| integration_id | Connected integration |
| connected_date | Connection timestamp  |

### Business Logic

Integration depth is a leading indicator of success.

Workspaces with 3+ integrations should demonstrate:

* Higher retention
* Higher automation adoption
* Higher conversion

---

## events

### Grain

One row per event.

### Estimated Volume

300,000-500,000 rows

### Purpose

Core behavioral fact table.

Supports nearly every KPI.

### Key Fields

| Column          | Description    |
| --------------- | -------------- |
| event_id        | Unique event   |
| workspace_id    | Workspace      |
| user_id         | User           |
| event_type      | Event category |
| event_timestamp | Timestamp      |

### Event Taxonomy

#### Activation

* workspace_created
* integration_connected
* workflow_generated

#### Engagement

* automation_created
* report_viewed
* task_completed

#### Collaboration

* invite_sent
* invite_accepted

#### Monetization

* plan_upgraded
* seat_added

#### Activity

* login
* session_started

### Business Logic

The majority of KPIs are derived from event behaviour rather than static attributes.

---

## invitations

### Grain

One row per invitation.

### Estimated Volume

20,000-40,000 rows

### Purpose

Measures collaboration and expansion.

Supports:

* Collaboration analysis
* Referral analysis
* Expansion analysis

### Key Fields

| Column         | Description           |
| -------------- | --------------------- |
| invitation_id  | Invitation identifier |
| workspace_id   | Origin workspace      |
| sender_user_id | Inviting user         |
| invite_date    | Sent date             |
| accepted_flag  | Accepted indicator    |

### Business Logic

Invitation activity should decline as activation quality deteriorates.

---

## subscriptions

### Grain

One row per subscription period.

### Estimated Volume

8,000-12,000 rows

### Purpose

Commercial fact table.

Supports:

* Conversion analysis
* Revenue analysis
* Expansion analysis

### Key Fields

| Column          | Description                 |
| --------------- | --------------------------- |
| subscription_id | Subscription identifier     |
| workspace_id    | Workspace                   |
| plan_type       | Free, Pro, Team, Enterprise |
| start_date      | Plan start                  |
| end_date        | Plan end                    |
| monthly_revenue | MRR contribution            |
| seats           | Active seats                |

### Business Logic

Conversion should be driven by product adoption rather than pricing.

This allows H5 (Pricing Friction) to emerge as a false lead.

---

# KPI Coverage Map

| KPI Category  | Primary Tables                 |
| ------------- | ------------------------------ |
| North Star    | events                         |
| Acquisition   | workspaces, users, channels    |
| Activation    | events, workspace_integrations |
| Engagement    | events                         |
| Collaboration | invitations, users, events     |
| Retention     | events, workspace_integrations |
| Monetization  | subscriptions, events          |
| Strategy      | workspaces, channels, events   |

---

# Hidden Causal Chain Encoding

The warehouse should naturally support the discovery of the following mechanism:

Acquisition Quality

↓

Activation Quality

↓

Integration Depth

↓

Automation Adoption

↓

Collaboration

↓

Retention

↓

Conversion

↓

Revenue Growth

The dataset should never explicitly store this chain.

The chain must emerge through analysis.

---

# Generation Constraints

The generated warehouse should satisfy the following conditions:

* Traffic remains healthy throughout the observation period.
* Referral share declines over time.
* Paid acquisition share increases over time.
* Activation weakens in newer cohorts.
* Integration depth declines in newer cohorts.
* Automation adoption weakens in newer cohorts.
* Invitation behavior declines in newer cohorts.
* Retention deterioration follows activation deterioration.
* Conversion deterioration follows retention deterioration.
* Revenue continues growing but at a slower rate.

These constraints ensure that multiple hypotheses appear plausible while preserving a single underlying mechanism.

---

# Design Goal

The warehouse should resemble the analytics environment of a real seed-to-Series-A SaaS company.

Every table, column, relationship, and event should exist because it helps answer a strategic business question related to growth, retention, monetization, or product adoption.

