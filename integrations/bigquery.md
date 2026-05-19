---
description: Connect your BigQuery project to Quper to track query costs and slot consumption.
icon: database
---

# Connect to BigQuery

Quper connects to BigQuery via a Service Account and tracks query costs, slot consumption, dataset storage, and spend by project, user, and dataset — giving data teams clear visibility into what is driving their BigQuery bill.

## What Quper tracks from BigQuery

- On-demand query costs by project, dataset, table, and user
- Slot consumption for flat-rate and reservation-based workloads
- Storage costs for active and long-term storage by dataset
- Query-level cost attribution — bytes processed, slot hours, and estimated cost per query
- Spend trends and anomalies in real time

## Before you begin

- You must have **Project Owner** or **BigQuery Admin** access in the GCP project you want to connect
- Quper supports connecting **multiple GCP projects** — repeat this process for each project, or connect at the billing account level via the [GCP integration](gcp.md) to cover all projects automatically

## Connection steps

{% stepper %}
{% step %}
#### Go to Settings → Integrations

In your Quper workspace, navigate to **Settings → Integrations** and click **Add Integration → BigQuery**.
{% endstep %}

{% step %}
#### Create a Service Account

In the Google Cloud Console, go to **IAM & Admin → Service Accounts** in your BigQuery project and create a new service account:

- Name: `quper-bigquery-reader`
- Description: Quper BigQuery read-only access
{% endstep %}

{% step %}
#### Grant the required roles

Grant the service account the following roles on the project:

| Role | Why it's needed |
|---|---|
| `BigQuery Data Viewer` | Read dataset, table, and job metadata |
| `BigQuery Job User` | Run INFORMATION_SCHEMA queries to pull usage data |
| `BigQuery Resource Viewer` | Read reservation and slot assignment data |
{% endstep %}

{% step %}
#### Download the service account key

On the service account details page, go to **Keys → Add Key → Create new key → JSON**. Download the key file.
{% endstep %}

{% step %}
#### Upload the key to Quper

Back in Quper, upload the JSON key file and enter your GCP Project ID. Click **Connect**.

Quper verifies the service account permissions and begins ingesting BigQuery cost and usage data.
{% endstep %}
{% endstepper %}

## How Quper calculates query costs

For **on-demand pricing**, Quper calculates query cost using the bytes processed by each job and GCP's published on-demand rate for your region.

For **flat-rate and reservation pricing**, Quper tracks slot-hour consumption per project and reservation, and maps it to your committed slot spend to show effective cost per query.

## Enabling INFORMATION_SCHEMA access

Quper uses BigQuery `INFORMATION_SCHEMA.JOBS` to pull per-query usage data. This view is available by default in all GCP projects. No additional setup is required.

{% hint style="info" %}
INFORMATION_SCHEMA job data is available for queries run in the **last 180 days**. Quper will backfill up to 90 days of data on initial connection.
{% endhint %}

## Troubleshooting

**"Access denied" on INFORMATION_SCHEMA queries**
Ensure the service account has `BigQuery Job User` at the project level. The `BigQuery Data Viewer` role alone is not sufficient to run INFORMATION_SCHEMA queries.

**Storage costs not appearing**
Confirm the service account has `BigQuery Data Viewer` at the project level. Dataset-level permissions are not sufficient for Quper to enumerate all datasets.
