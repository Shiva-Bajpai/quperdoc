---
description: Get a complete breakdown of every dollar spent across your cloud — in real time.
icon: chart-bar
---

# Spend Overview

Spend Overview is Quper's unified cost dashboard. It gives you a complete, real-time picture of what you are spending across every connected cloud provider and data platform — broken down by service, account, region, team, and tag.

## What you can do in Spend Overview

- **See your total spend** at a glance — current week, month, quarter, or custom date range
- **Compare spend periods** — week-over-week, month-over-month, or against any historical window
- **Drill down by dimension** — filter by cloud provider, service, account, region, resource tag, or team
- **View daily and hourly resolution** — see exactly when spend spiked and which service drove it
- **Spot anomalies inline** — active cost anomalies are surfaced directly in the spend chart with markers
- **Export data** — download spend breakdowns as CSV for finance and stakeholder reporting

## Spend breakdown dimensions

Quper organises your cloud spend by the following dimensions. You can filter and group by any combination:

| Dimension | Description |
|---|---|
| **Provider** | The cloud provider or data platform (AWS, GCP, Azure, Snowflake, Databricks, BigQuery) |
| **Account / Project** | The billing account, GCP project, or Azure subscription |
| **Service** | The specific cloud service (e.g. EC2, Cloud Storage, Azure SQL) |
| **Region** | The geographic region where the resource runs |
| **Resource** | The individual resource instance (where available) |
| **Tag** | Any resource tag or label applied in your cloud environment |
| **Team** | A team-level attribution based on Quper governance policies |

## Reading the spend chart

The main chart in Spend Overview shows your daily spend as a bar chart. Each bar represents one day of total spend across all connected platforms.

- **Blue bars** — normal spend within expected range
- **Red markers** — days with active anomalies detected by Quper
- **Dotted line** — your average daily spend over the selected period (run rate)

Hover over any bar to see a breakdown of that day's spend by service or dimension.

## Top Services by spend

Below the chart, Quper displays a ranked list of your top cost drivers for the selected period. Each service shows:

- Total spend in the period
- Percentage of total spend
- Trend vs. previous period (up, down, or flat)
- An indicator if an anomaly is currently active on that service

Click any service to drill into its cost history and resource-level breakdown.

## Filters and saved views

Use the filter bar at the top of Spend Overview to narrow the view by any dimension. You can combine multiple filters — for example, filtering to a specific AWS account in us-east-1 with the tag `team:data-engineering`.

Save frequently used filter combinations as **Saved Views** for quick access. Saved Views can be made private (personal) or shared with your team.

## Limitations

- Spend data is updated every **24 hours** for cloud provider billing, and every **hour** for real-time usage signals
- Historical data is available for the last **12 months** after initial connection. Data older than 12 months is available on request
- Resource-level attribution (down to individual EC2 instances or queries) requires resource-level tagging to be enabled in your cloud environment

## What's next

{% content-ref url="../detect/anomalies.md" %}
[anomalies.md](../detect/anomalies.md)
{% endcontent-ref %}

{% content-ref url="../decide/action-intelligence.md" %}
[action-intelligence.md](../decide/action-intelligence.md)
{% endcontent-ref %}

{% content-ref url="../govern/cost-governance.md" %}
[cost-governance.md](../govern/cost-governance.md)
{% endcontent-ref %}
