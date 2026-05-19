---
description: Set budgets, enforce tag policies, and prevent ungoverned cloud growth.
icon: shield-check
---

# Cost Governance

Cost Governance is Quper's policy enforcement layer. It lets you define the rules for how cloud spend should be managed — budgets, tag requirements, team ownership — and then enforces those rules automatically, alerting your team when policies are breached and preventing ungoverned cloud growth before it compounds.

## Governance Score

Quper calculates a **Governance Score** (0–100) for your organisation that reflects how well your cloud environment adheres to your defined policies. The score is updated daily and broken down by policy category.

A higher score means more of your infrastructure is governed, tagged, owned, and within budget. Quper shows the score on the Govern dashboard alongside the dollar value of spend that was automatically saved or prevented through policy enforcement.

## Budget Limits

Set team-level or service-level budgets to enforce cost ownership across your organisation.

### Creating a budget

1. Go to **Govern → Cost Governance → Budgets**
2. Click **Create Budget**
3. Define the scope — by cloud provider, account, service, tag, or team
4. Set the budget amount and period (monthly or custom)
5. Configure alert thresholds — e.g. alert at 70%, 90%, and 100% of budget
6. Assign budget owners — the users or teams who will be notified on breach

### Budget alerts

When spend reaches a configured threshold, Quper notifies the budget owner via their preferred channel (email, Slack, or Teams). Notifications include:

- Current spend vs. budget
- Projected end-of-period spend (run rate)
- Top services driving the overage

### Budget enforcement

Beyond alerts, Quper can enforce hard budget caps for supported platforms. When a hard cap is reached, Quper can automatically pause non-critical workloads or trigger a webhook to your automation system for custom enforcement logic.

## Tag Policies

Enforce tagging standards across your cloud environment to ensure every resource has an owner, team, environment, and cost centre.

### Creating a tag policy

1. Go to **Govern → Cost Governance → Tag Policies**
2. Click **Create Policy**
3. Define the required tags — e.g. `team`, `environment`, `cost-centre`, `owner`
4. Set the scope — which cloud provider, account, or service the policy applies to
5. Set the enforcement action — Alert only, or Alert + Block untagged resources from being tracked

### Tag compliance reporting

Quper shows tag coverage as a percentage of total spend. Resources without required tags are listed in the **Tag Gaps** view with their cost contribution, so your team can prioritise which untagged resources to fix first based on spend impact.

Governance reports showing tag compliance are exportable as PDF or CSV for finance and executive reviews.

## Team Ownership

Assign cloud resources to teams so that every dollar of spend has a clear owner. Team ownership works alongside tag policies — Quper uses resource tags to automatically map spend to teams, and flags any spend that cannot be attributed to an owner.

### Setting up team ownership

1. Go to **Govern → Teams**
2. Create a team and define its tag-based attribution rules (e.g. all resources tagged `team:data-engineering` belong to the Data Engineering team)
3. Assign team members — they will receive budget alerts and governance reports for their team's spend
4. Set team budgets and tag requirements specific to that team

## Governance Reports

Quper generates weekly governance reports that summarise:

- Current Governance Score and trend
- Budget status across all active budgets
- Tag compliance percentage and top untagged resources by spend
- Policies that were breached in the last 7 days
- Dollar value saved through policy enforcement

Reports are delivered to configured recipients automatically each week and are available for export at any time from the Govern dashboard.

## Limitations

- Hard budget enforcement (automatic workload pausing) is currently supported for Snowflake and Databricks only
- Tag compliance scanning runs every 24 hours — newly created untagged resources may take up to 24 hours to appear in the Tag Gaps view
- A maximum of **50 active budget policies** and **20 active tag policies** are supported per workspace

## FAQs

**What is a good Governance Score target?**
Most FinOps-mature teams aim for a score of 80 or above. A score of 90+ indicates that nearly all spend is governed, attributed, and within budget. Quper's recommendations in the Decide section will help you close the gaps.

**Can I create governance policies for a subset of accounts?**
Yes. Policies can be scoped to specific cloud accounts, GCP projects, Azure subscriptions, or Snowflake accounts. You can also scope by tag values to target specific environments (e.g. production only).

**How is the Governance Score calculated?**
The score is a weighted average of four components: budget compliance (30%), tag coverage by spend (30%), team attribution coverage (20%), and idle resource ratio (20%). The weights reflect the typical impact of each factor on cloud cost control.
