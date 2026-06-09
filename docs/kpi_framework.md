# KPI Framework

## Purpose

This project investigates why growth slowed at SynapseOS despite healthy traffic and continued revenue growth.

KPIs are selected to answer leadership questions, evaluate competing hypotheses, and identify the root cause of the slowdown.

The framework prioritizes actionable metrics over vanity metrics. Every KPI must contribute to a business decision.

---

# KPI Philosophy

### Principles

1. Measure business outcomes before operational activity.
2. Prioritize metrics that explain growth, not just describe it.
3. Use KPIs to test hypotheses.
4. Avoid vanity metrics such as total users, page views, or total events.
5. Focus on leading indicators before lagging indicators.

---

# Executive KPI Tree

Growth slowdown is investigated through the following causal chain:

Acquisition Quality → Activation Quality → Integration Depth → Automation Adoption → Collaboration → Retention → Conversion → Revenue Growth

---

# North Star Metrics

| KPI                            | Business Question                         | Formula                                     | Grain  | Source |
| ------------------------------ | ----------------------------------------- | ------------------------------------------- | ------ | ------ |
| Weekly Active Workspaces (WAW) | Are workspaces receiving recurring value? | Distinct active workspaces per week         | Weekly | events |
| WAW Growth Rate                | Is product usage growing or slowing?      | (Current WAW - Previous WAW) / Previous WAW | Weekly | events |

---

# Acquisition KPIs

| KPI                        | Business Question                  | Formula                               | Grain   | Source              |
| -------------------------- | ---------------------------------- | ------------------------------------- | ------- | ------------------- |
| New Workspaces by Channel  | Which channels drive acquisition?  | Count of new workspaces by channel    | Monthly | workspaces          |
| Acquisition Mix %          | Has channel composition changed?   | Channel workspaces / Total workspaces | Monthly | workspaces          |
| Activation Rate by Channel | Are newer channels lower quality?  | Activated workspaces / New workspaces | Monthly | workspaces, events  |
| CAC                        | Is growth becoming more expensive? | Marketing Spend / New Customers       | Monthly | external assumption |

### Supports

* H1 Acquisition Quality Decline

---

# Activation KPIs

| KPI                                 | Business Question                       | Formula                                            | Grain  | Source                 |
| ----------------------------------- | --------------------------------------- | -------------------------------------------------- | ------ | ---------------------- |
| Activation Rate                     | Are users reaching initial value?       | Activated workspaces / New workspaces              | Cohort | workspaces, events     |
| Time-to-Activation                  | Is onboarding becoming harder?          | Avg. days to activation                            | Cohort | events                 |
| Integration Depth                   | How embedded is the product?            | Avg. integrations per workspace                    | Cohort | workspace_integrations |
| Workspaces with 3+ Integrations (%) | Are users reaching meaningful adoption? | Workspaces with ≥3 integrations / Total workspaces | Cohort | workspace_integrations |
| Workflow Creation Rate              | Are users configuring workflows?        | Workspaces creating workflows / Total workspaces   | Cohort | events                 |

### Supports

* H2 Onboarding Complexity

---

# Engagement KPIs

| KPI                             | Business Question                         | Formula                                         | Grain   | Source |
| ------------------------------- | ----------------------------------------- | ----------------------------------------------- | ------- | ------ |
| Automation Adoption Rate        | Are users adopting the core value driver? | Workspaces using automation / Active workspaces | Monthly | events |
| Automation Intensity            | How deeply is automation used?            | Automations created / Active workspace          | Monthly | events |
| Reports Generated per Workspace | Is usage becoming embedded in operations? | Reports generated / Active workspace            | Monthly | events |

### Supports

* H3 Automation Adoption Decline

---

# Collaboration KPIs

| KPI                    | Business Question             | Formula                                  | Grain   | Source      |
| ---------------------- | ----------------------------- | ---------------------------------------- | ------- | ----------- |
| Invitation Rate        | Are users inviting teammates? | Invitations sent / Active workspace      | Monthly | invitations |
| Invite Acceptance Rate | Are invitations converting?   | Accepted invites / Sent invites          | Monthly | invitations |
| Multi-User Workspace % | Are workspaces collaborative? | Multi-user workspaces / Total workspaces | Monthly | users       |
| Average Team Size      | Are workspaces expanding?     | Users per workspace                      | Monthly | users       |

### Supports

* H4 Collaboration Loop Weakening

---

# Retention KPIs

| KPI                            | Business Question                       | Formula                                   | Grain  | Source                         |
| ------------------------------ | --------------------------------------- | ----------------------------------------- | ------ | ------------------------------ |
| Week 4 Retention               | Are users staying after onboarding?     | Retained at Week 4 / Activated users      | Cohort | events                         |
| Week 8 Retention               | Does value persist over time?           | Retained at Week 8 / Activated users      | Cohort | events                         |
| Retention by Activation Status | Does activation drive retention?        | Retention segmented by activation outcome | Cohort | events                         |
| Retention by Integration Depth | Does deeper adoption improve retention? | Retention segmented by integration depth  | Cohort | workspace_integrations, events |

### Supports

* H2 Onboarding Complexity
* H3 Automation Adoption Decline
* H4 Collaboration Loop Weakening

---

# Monetization KPIs

| KPI                             | Business Question                        | Formula                                    | Grain   | Source                |
| ------------------------------- | ---------------------------------------- | ------------------------------------------ | ------- | --------------------- |
| Free-to-Paid Conversion Rate    | Are users willing to pay?                | Paid workspaces / Eligible free workspaces | Monthly | subscriptions         |
| Conversion by Activation Status | Is value realization driving conversion? | Conversion segmented by activation outcome | Cohort  | subscriptions, events |
| Paid Workspace Rate             | What share of workspaces monetize?       | Paid workspaces / Total workspaces         | Monthly | subscriptions         |
| Expansion Rate                  | Are paid accounts growing?               | Workspaces adding seats / Paid workspaces  | Monthly | subscriptions, events |
| Monthly Recurring Revenue (MRR) | How is revenue performing?               | Sum of recurring subscription revenue      | Monthly | subscriptions         |

### Supports

* H5 Pricing Friction

---

# Strategic KPIs

| KPI                                | Business Question                                       | Formula                                           | Grain   | Source     |
| ---------------------------------- | ------------------------------------------------------- | ------------------------------------------------- | ------- | ---------- |
| Referral Share                     | Is the organic growth engine weakening?                 | Referral workspaces / Total workspaces            | Monthly | workspaces |
| Referral Generation Rate           | Are retained users creating new growth?                 | Referral workspaces generated / Active workspaces | Monthly | workspaces |
| Activation-to-Retention Conversion | How efficiently is activation becoming long-term usage? | Retained users / Activated users                  | Cohort  | events     |

### Supports

* H1 Acquisition Quality Decline
* H4 Collaboration Loop Weakening
* H6 Market Saturation

---

# Hypothesis Mapping

| Hypothesis                      | Primary KPIs                                                                                                 |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| H1 Acquisition Quality Decline  | Acquisition Mix %, Activation Rate by Channel, CAC, Referral Share                                           |
| H2 Onboarding Complexity        | Activation Rate, Time-to-Activation, Integration Depth, 3+ Integrations %, Workflow Creation Rate            |
| H3 Automation Adoption Decline  | Automation Adoption Rate, Automation Intensity                                                               |
| H4 Collaboration Loop Weakening | Invitation Rate, Invite Acceptance Rate, Multi-User Workspace %, Average Team Size, Referral Generation Rate |
| H5 Pricing Friction             | Free-to-Paid Conversion Rate, Conversion by Activation Status                                                |
| H6 Market Saturation            | Referral Share, New Workspaces by Channel                                                                    |

---

# Decision Framework

Each KPI must inform a decision.

Examples:

* Falling activation rate → Simplify onboarding and integration setup.
* Falling integration depth → Improve activation guidance and integration recommendations.
* Falling automation adoption → Improve workflow templates and activation flows.
* Falling invitation rate → Improve collaboration onboarding.
* Falling retention among low-activation cohorts → Prioritize activation improvements over pricing changes.
* Falling conversion despite stable activation → Investigate pricing and packaging.

The objective is not to monitor metrics. The objective is to identify the highest-leverage intervention that restores sustainable growth.
