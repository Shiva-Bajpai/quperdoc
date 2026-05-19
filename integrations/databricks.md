---
description: Connect your Databricks workspace to Quper to track cluster and job costs.
icon: database
---

# Connect to Databricks

Quper connects to Databricks via a Personal Access Token and tracks cluster spend, job costs, DBU consumption, and idle compute — so your data engineering teams have full visibility into what every pipeline and notebook is costing.

## What Quper tracks from Databricks

- Cluster-level DBU (Databricks Unit) consumption and dollar cost
- Job run costs — spend per job, run, and task
- Interactive cluster vs. job cluster cost split
- Idle cluster time and auto-termination gaps
- Cost breakdown by workspace, cluster policy, and team tag
- Spot vs. on-demand instance cost attribution

## Before you begin

- You must have **workspace admin** access to create a service principal or personal access token
- Quper supports connecting **multiple Databricks workspaces** — repeat this process for each workspace

## Connection steps

{% stepper %}
{% step %}
#### Go to Settings → Integrations

In your Quper workspace, navigate to **Settings → Integrations** and click **Add Integration → Databricks**.
{% endstep %}

{% step %}
#### Create a Personal Access Token

In your Databricks workspace, go to **User Settings → Access Tokens** and click **Generate New Token**:

- Comment: `Quper read-only access`
- Lifetime: 365 days (recommended — rotate annually)
- Click **Generate**

Copy the token value — Databricks will not show it again.
{% endstep %}

{% step %}
#### Enter credentials in Quper

Back in Quper, enter:

- **Workspace URL** — your Databricks workspace URL (e.g. `https://dbc-abc12345-6789.cloud.databricks.com`)
- **Access Token** — the token you generated above
- **Cloud Provider** — the cloud platform your Databricks workspace runs on (AWS, GCP, or Azure)

Click **Connect**. Quper verifies the token and begins ingesting cluster and job cost data.
{% endstep %}
{% endstepper %}

## Limitations

- Quper reads cluster and job cost data via the Databricks REST API and System Tables. System Tables must be enabled in your workspace for full query-level attribution.
- Cost data for job runs is available after the run completes. In-progress jobs appear in usage data but final cost is confirmed on completion.
- Quper does not support Databricks on-premises deployments.

## Enabling System Tables (recommended)

Databricks System Tables provide the most granular cost and usage data. To enable them:

1. In your Databricks workspace, go to **Catalog → System** (requires Unity Catalog)
2. Enable the `system.billing`, `system.compute`, and `system.lakeflow` schemas
3. Grant the Quper service principal `SELECT` access on these schemas

{% hint style="info" %}
System Tables require **Unity Catalog**. If your workspace does not have Unity Catalog enabled, Quper will fall back to the Cluster Events API and Jobs API for cost data, which provides less granularity.
{% endhint %}

## Troubleshooting

**Token authentication fails**
Verify the workspace URL does not have a trailing slash and matches the URL you use to access Databricks in your browser.

**Job costs not appearing**
Ensure the Quper token has at least `CAN_VIEW` permission on the jobs and clusters you want to track. Quper cannot see job runs it doesn't have permission to list.
