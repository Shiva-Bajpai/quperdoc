---
description: Connect Quper to your cloud providers, data warehouses, and data platforms.
icon: plug
---

# Overview

Quper connects directly to your infrastructure using secure, read-only access — with no agents to install and no disruption to your existing setup.

## Supported integrations

### Cloud Providers

Connect your cloud billing to Quper to get a unified view of compute, storage, networking, and managed service spend across all your accounts and regions.

| Provider                                     | What Quper tracks                                                                              |
| -------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| [AWS](cloud-providers/aws.md)                | EC2, RDS, Lambda, S3, EKS, and all other AWS services via Cost and Usage Reports               |
| [Google Cloud (GCP)](cloud-providers/gcp.md) | Compute Engine, BigQuery, Cloud Storage, GKE, and all GCP services via Billing Export          |
| [Microsoft Azure](cloud-providers/azure.md)  | Virtual Machines, Azure SQL, Blob Storage, AKS, and all Azure services via Cost Management API |

### Data Warehouses & Platforms

Connect your data platforms to Quper to track query costs, warehouse utilisation, and job-level spend in real time.

| Platform                                                  | What Quper tracks                                                                                    |
| --------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| [Snowflake](data-warehouses-and-platforms/snowflake.md)   | Warehouse credits, storage costs, query spend, idle compute, and credit consumption by user and role |
| [Databricks](data-warehouses-and-platforms/databricks.md) | Cluster spend, job costs, DBU consumption, idle clusters, and cost by workspace and team             |
| [BigQuery](data-warehouses-and-platforms/bigquery.md)     | Slot consumption, on-demand query costs, dataset storage, and spend by project and user              |

## How integrations work

Quper pulls data from each connected platform on a regular cadence:

* **Cloud providers** — billing and usage data is refreshed every 24 hours, with real-time usage signals updated every hour
* **Data warehouses** — query-level cost data is updated every hour; storage data is updated every 24 hours

After connecting a new integration, Quper automatically backfills **90 days** of historical cost and usage data.

## Adding a new integration

1. Go to **Settings → Integrations**
2. Click **Add Integration**
3. Select your provider or platform
4. Follow the step-by-step connection guide

Each integration requires read-only credentials only. Quper never requests or stores write access to your infrastructure.

## Removing an integration

1. Go to **Settings → Integrations**
2. Find the integration you want to remove
3. Click the options menu (⋯) and select **Disconnect**
4. Confirm the disconnection

After disconnecting, Quper retains your historical cost data but stops ingesting new data from that source.

{% hint style="info" %}
You can reconnect a previously disconnected integration at any time. Quper will resume data ingestion from the point of reconnection and backfill any gap in data.
{% endhint %}
