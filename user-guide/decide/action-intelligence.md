---
description: Prioritised AI recommendations that tell you exactly what to fix and why it matters.
icon: bolt
---

# Action Intelligence

Action Intelligence is Quper's recommendation engine. It surfaces prioritised, impact-ranked optimisation opportunities across all your connected cloud providers and data platforms — so your team knows exactly what to fix, in what order, and what it will save.

Every recommendation comes from Vidura AI, which continuously analyses your usage patterns, compares them against efficiency benchmarks, and generates concrete actions with estimated savings.

## What Quper recommends

Quper generates recommendations across four categories:

### Rightsizing
Resources that are consistently over-provisioned relative to their actual utilisation. Quper identifies instances, warehouses, or clusters running at low utilisation and recommends a smaller configuration.

Examples:
- EC2 instance running at 8% average CPU → downsize from `m5.2xlarge` to `m5.large`
- Snowflake warehouse at 12% average utilisation → resize from Large to Small
- Databricks cluster with 4 workers but only using 1 → reduce worker count

### Idle Resources
Resources that are running but consuming spend without active workloads.

Examples:
- EC2 instance with zero network traffic and zero CPU for 72+ hours → terminate or stop
- Snowflake warehouse with no queries for 4+ hours and auto-suspend disabled → enable auto-suspend
- Databricks interactive cluster running overnight with no attached notebooks → enable auto-termination

### Commitment Optimisation
Opportunities to replace on-demand spend with Reserved Instances, Savings Plans, or committed use discounts for predictable workloads.

Examples:
- EC2 workload with 90%+ on-demand usage over the past 30 days → purchase a 1-year Reserved Instance
- Databricks compute with consistent DBU consumption → purchase a DBU commitment

### Configuration Fixes
Simple misconfigurations that are causing unnecessary spend.

Examples:
- Snowflake warehouse with auto-suspend disabled running 24/7 → enable auto-suspend with 10-minute idle timeout
- S3 buckets with no lifecycle policy → add lifecycle rules to transition old objects to Glacier
- BigQuery tables with no partition expiry → set expiry on large datasets

## The recommendations list

Navigate to **Decide → Action Intelligence** to see your full list of recommendations.

Each recommendation shows:

- **Resource** — the specific service and resource affected
- **Issue** — what Quper found and why it is causing unnecessary spend
- **Estimated monthly savings** — projected savings if the recommendation is applied
- **Effort** — Low, Medium, or High based on the complexity of applying the fix
- **Action** — a one-click action for eligible fixes, or step-by-step instructions for manual changes

Recommendations are sorted by estimated monthly savings by default. You can re-sort by effort, resource type, or cloud provider.

## Applying a recommendation

For eligible resources, Quper provides one-click application of the recommended change:

1. Click **Optimise** on the recommendation
2. Review the proposed change — Quper shows exactly what will be modified
3. Click **Apply** to confirm
4. Quper applies the change and updates the recommendation status to **Applied**

One-click actions are available for:
- Snowflake warehouse resize
- Snowflake warehouse auto-suspend configuration
- Databricks cluster auto-termination configuration

For AWS, GCP, and Azure resources, Quper provides the recommended action with detailed steps to apply it in your cloud console. Full one-click support for cloud provider resources is on the roadmap.

## Decision trails

Every applied recommendation is logged in the **Decision Trail** — an audit history that records:

- What was changed
- When it was applied
- Who applied it
- The estimated vs. actual savings after 30 days

Decision trails are available for export and are useful for finance reviews, engineering retrospectives, and demonstrating FinOps impact to leadership.

## Limitations

- Savings estimates are projections based on current usage patterns. Actual savings may vary if workload patterns change.
- Commitment optimisation recommendations require at least **30 days of usage history** before Quper will suggest a commitment purchase.
- One-click apply is currently supported for Snowflake and Databricks only. AWS, GCP, and Azure one-click actions are on the roadmap.

## FAQs

**How often are recommendations refreshed?**
Recommendations are recalculated every 24 hours based on the latest usage data. A recommendation is automatically removed once the underlying issue is resolved.

**What if I don't want to act on a recommendation?**
You can dismiss a recommendation with a reason (e.g. "Workload is scheduled to increase next quarter"). Dismissed recommendations are hidden from the main list but remain in your recommendation history.

**Can I see the impact of recommendations I've already applied?**
Yes. Go to the **Decision Trail** to see every applied recommendation and its confirmed savings after 30 days of monitoring.
