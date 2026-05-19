---
description: Connect your Google Cloud account to Quper via a Service Account.
icon: cloud
---

# Connect to GCP

Quper connects to Google Cloud using a Service Account with read-only Billing Viewer permissions. The service account is scoped to your billing account and cannot modify any GCP resources.

## What Quper tracks from GCP

- All GCP service costs via Cloud Billing Export to BigQuery
- Compute Engine, Cloud Storage, BigQuery, GKE, Cloud Run, and all other GCP services
- Cost and usage broken down by project, service, region, SKU, and label
- Committed Use Discount (CUD) utilisation and coverage
- Hourly spend signals for real-time anomaly detection

## Before you begin

- You must have **Billing Account Administrator** access in GCP
- Cloud Billing Export to BigQuery must be enabled in your billing account (Quper can help set this up if it isn't already)
- Quper supports connecting **multiple GCP projects** under the same billing account automatically

## Connection steps

{% stepper %}
{% step %}
#### Go to Settings → Integrations

In your Quper workspace, navigate to **Settings → Integrations** and click **Add Integration → GCP**.
{% endstep %}

{% step %}
#### Create a Service Account

In the Google Cloud Console, go to **IAM & Admin → Service Accounts** and create a new service account:

- Name: `quper-readonly`
- Description: Quper read-only billing access

Grant the service account the following roles at the **billing account** level:
- `Billing Account Viewer`
- `BigQuery Data Viewer` (on the billing export dataset)
- `BigQuery Job User` (on the project containing the billing dataset)
{% endstep %}

{% step %}
#### Download the service account key

On the service account details page, go to **Keys → Add Key → Create new key** and select **JSON**. Download the key file.

{% hint style="info" %}
Store this key file securely. Quper only needs it during setup and stores the credentials encrypted at rest.
{% endhint %}
{% endstep %}

{% step %}
#### Upload the key to Quper

Back in Quper, upload the JSON key file and enter your GCP Billing Account ID (found in **Billing → Account Management**). Click **Connect**.

Quper verifies the service account permissions and begins initial data ingestion.
{% endstep %}
{% endstepper %}

## Enabling Cloud Billing Export

If you haven't already enabled Cloud Billing Export to BigQuery, Quper will prompt you to do so during setup. To enable it manually:

1. In the Google Cloud Console, go to **Billing → Billing Export**
2. Click **Edit Settings** under BigQuery Export
3. Select your project and create or choose a BigQuery dataset
4. Enable **Standard usage cost** and **Detailed usage cost** exports
5. Click **Save**

{% hint style="info" %}
It can take up to **24 hours** after enabling Billing Export for the first data to appear in BigQuery and in Quper.
{% endhint %}

## Troubleshooting

**"Permission denied" error during connection**
Confirm the service account has been granted Billing Account Viewer at the billing account level (not just the project level). Billing account roles are set in **Billing → Account Management → Permissions**, not in IAM.

**No data appearing after 24 hours**
Verify that Cloud Billing Export is enabled and that the BigQuery dataset name entered in Quper matches the dataset where your billing export is writing data.
