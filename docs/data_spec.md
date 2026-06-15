# Data Generation Specification

## Purpose

This document defines the quantitative assumptions used to generate the SynapseOS analytical warehouse.

---
## Dataset Scale

| Entity               |          Volume |
| -------------------- | --------------: |
| Workspaces           |           8,000 |
| Users                |          25,000 |
| Events               | 300,000-500,000 |
| Invitations          |   20,000-40,000 |
| Subscription Records |    8,000-12,000 |

---

# Cohort Allocation

| Phase        | Months | Workspaces |
| ------------ | ------ | ---------: |
| Early Growth | 1-6    |      2,500 |
| Expansion    | 7-9    |      1,500 |
| Slowdown     | 10-18  |      4,000 |

---

# Acquisition Mix

## Months 1-6

| Channel             | Share |
| ------------------- | ----: |
| Referral            |   35% |
| Product Hunt        |   25% |
| Startup Communities |   25% |
| LinkedIn Ads        |   10% |
| Google Ads          |    5% |

## Months 7-9

| Channel             | Share |
| ------------------- | ----: |
| Referral            |   25% |
| Product Hunt        |   15% |
| Startup Communities |   25% |
| LinkedIn Ads        |   20% |
| Google Ads          |   15% |

## Months 10-18

| Channel             | Share |
| ------------------- | ----: |
| Referral            |   15% |
| Product Hunt        |   10% |
| Startup Communities |   20% |
| LinkedIn Ads        |   30% |
| Google Ads          |   25% |

---

# Activation Rates

| Channel             | Activation Rate |
| ------------------- | --------------: |
| Referral            |             64% |
| Product Hunt        |             60% |
| Startup Communities |             56% |
| LinkedIn Ads        |             50% |
| Google Ads          |             46% |

Activation criteria:

* ≥2 integrations connected
* ≥1 workflow generated
* Within 14 days of workspace creation

---

# Integration Depth Distribution

| Channel             | 0-2 | 3-4 |  5+ |
| ------------------- | --: | --: | --: |
| Referral            | 25% | 50% | 25% |
| Product Hunt        | 35% | 45% | 20% |
| Startup Communities | 40% | 45% | 15% |
| LinkedIn Ads        | 50% | 40% | 10% |
| Google Ads          | 55% | 35% | 10% |

---

# Automation Adoption

| Integration Segment | Adoption Rate |
| ------------------- | ------------: |
| 0-2 Integrations    |           20% |
| 3-4 Integrations    |           45% |
| 5+ Integrations     |           65% |

---

# Collaboration

Invitation probability:

| Segment         | Rate |
| --------------- | ---: |
| No Automation   |  30% |
| Automation User |  55% |

Average invitations per inviting workspace:

| Segment         | Invitations |
| --------------- | ----------: |
| No Automation   |           2 |
| Automation User |           3 |

Invite acceptance rate: **70%**

---

# Retention

## Week 4

| Segment                     | Retention |
| --------------------------- | --------: |
| Not Activated               |       35% |
| Activated                   |       55% |
| Activated + 3+ Integrations |       65% |

## Week 8

| Segment                     | Retention |
| --------------------------- | --------: |
| Not Activated               |       20% |
| Activated                   |       42% |
| Activated + 3+ Integrations |       55% |

---

# Conversion

| Segment                             | Conversion Rate |
| ----------------------------------- | --------------: |
| Not Activated                       |              3% |
| Activated                           |              8% |
| Activated + Automation              |             14% |
| Activated + Automation + Multi-User |             20% |

---

# Expansion

| Segment     | Expansion Rate |
| ----------- | -------------: |
| Single User |             5% |
| Multi-User  |            20% |

Average seats added:

| Segment     | Seats Added |
| ----------- | ----------: |
| Single User |           1 |
| Multi-User  |           3 |

---

# Plan Mix

| Plan       | Share |
| ---------- | ----: |
| Pro        |   65% |
| Team       |   30% |
| Enterprise |    5% |

---

# Pricing

| Plan       | Monthly Revenue |
| ---------- | --------------: |
| Pro        |             $19 |
| Team       |   $99 + $8/user |
| Enterprise |            $600 |

---

# Event Types

### Activation

* workspace_created
* integration_connected
* workflow_generated

### Engagement

* automation_created
* report_viewed
* task_completed

### Collaboration

* invite_sent
* invite_accepted

### Monetization

* plan_upgraded
* seat_added

### Activity

* login
* session_started

---

# Noise Parameters

| Condition                               | Rate |
| --------------------------------------- | ---: |
| Low-engagement users who retain         |  10% |
| High-engagement users who churn         |  10% |
| Low-engagement users who convert        |   5% |
| High-engagement users who never convert |   5% |

---

# Validation Targets

| Metric                 | Expected Trend                   |
| ---------------------- | -------------------------------- |
| Referral Share         | Declining                        |
| Paid Acquisition Share | Increasing                       |
| Activation Rate        | Declining                        |
| Integration Depth      | Declining                        |
| Automation Adoption    | Declining                        |
| Invitation Rate        | Declining                        |
| Retention              | Declining                        |
| Conversion             | Declining                        |
| WAW Growth             | Slowing                          |
| MRR                    | Growing, Slower Than User Growth |
