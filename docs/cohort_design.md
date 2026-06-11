# Cohort Design

## Purpose

This document defines the behavioural differences across acquisition channels and time-based cohorts used in the SynapseOS warehouse simulation.

The goal is to encode realistic growth dynamics while preserving multiple plausible explanations for the observed slowdown.

---

# Observation Period

| Phase        | Months | Description                                        |
| ------------ | ------ | -------------------------------------------------- |
| Early Growth | 1-6    | Strong PMF and high-quality acquisition            |
| Expansion    | 7-9    | Marketing scales after seed funding                |
| Slowdown     | 10-18  | Growth continues but customer quality deteriorates |

---

# Acquisition Channel Quality

| Channel             | Relative Quality |
| ------------------- | ---------------- |
| Referral            | Highest          |
| Product Hunt        | High             |
| Startup Communities | Medium-High      |
| LinkedIn Ads        | Medium           |
| Google Ads          | Lowest           |

Expected characteristics:

* Referral users activate, retain, and convert best.
* Paid channels underperform organic and referral channels.
* Google Ads produces the weakest downstream outcomes.

---

# Acquisition Mix Evolution

| Phase        | Referral | Product Hunt | Communities | LinkedIn Ads | Google Ads |
| ------------ | -------: | -----------: | ----------: | -----------: | ---------: |
| Months 1-6   |     High |         High |      Medium |          Low |        Low |
| Months 7-9   |   Medium |       Medium |      Medium |      Growing |    Growing |
| Months 10-18 |    Lower |        Lower |      Medium |         High |       High |

Result:

Traffic remains healthy while average customer quality declines.

---

# Activation

### Activation Definition

A workspace is activated when:

* ≥2 integrations are connected
* ≥1 workflow is generated
* Actions occur within 14 days of signup

### Cohort Trend

| Cohort       | Activation |
| ------------ | ---------- |
| Months 1-6   | High       |
| Months 7-9   | Moderate   |
| Months 10-18 | Lower      |

Activation deterioration should appear before retention deterioration.

---

# Integration Depth

| Segment  | Integrations Connected |
| -------- | ---------------------- |
| Shallow  | 0-2                    |
| Moderate | 3-4                    |
| Deep     | 5+                     |

Workspaces with 3+ integrations are significantly more likely to:

* Create automations
* Invite teammates
* Retain
* Convert

---

# Automation Adoption

| Cohort       | Adoption       |
| ------------ | -------------- |
| Months 1-6   | High           |
| Months 7-9   | Slightly Lower |
| Months 10-18 | Lower          |

Automation adoption should strongly correlate with integration depth and long-term retention.

---

# Collaboration

Expected behaviour:

* Deeply integrated workspaces invite more teammates.
* Automation users exhibit stronger collaboration.
* Weakly activated workspaces remain single-user.

Primary signals:

* Invitations sent
* Invitation acceptance
* Team growth
* Seat expansion

---

# Retention

Retention should emerge from behaviour rather than be assigned directly.

Positive drivers:

* Activation
* Integration depth
* Automation adoption
* Team collaboration

Expected trend:

| Cohort       | Retention      |
| ------------ | -------------- |
| Months 1-6   | Strong         |
| Months 7-9   | Slightly Lower |
| Months 10-18 | Lower          |

Retention decline should lag activation decline.

---

# Conversion

Conversion should primarily depend on realized value rather than pricing.

Primary drivers:

* Activation
* Integration depth
* Automation adoption
* Collaboration

This allows pricing friction to emerge as a plausible but ultimately incorrect explanation.

---

# Referral Generation

Referral likelihood increases with:

* Retention
* Automation adoption
* Team adoption

As product adoption weakens, referral growth naturally slows.

---

# Behavioural Logic

The simulation should support the discovery of the following mechanism:

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

The relationship should emerge through analysis rather than be explicitly encoded in any single table.
