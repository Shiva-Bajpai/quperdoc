---
description: Connect your Azure subscription to Quper via App Registration.
icon: cloud
---

# Connect to Azure

Quper connects to Azure using an App Registration (service principal) with the Cost Management Reader role. This grants read-only access to your billing and usage data across subscriptions.

## What Quper tracks from Azure

- All Azure service costs via the Cost Management API
- Virtual Machines, Azure SQL, Blob Storage, AKS, App Service, and all other Azure services
- Cost and usage broken down by subscription, resource group, resource, region, and tag
- Azure Reservations utilisation and coverage
- Hourly spend signals for real-time anomaly detection

## Before you begin

- You must have **Owner** or **User Access Administrator** access on the Azure subscription or Management Group you want to connect
- Quper supports connecting **multiple subscriptions** — you can connect at the Management Group level to cover all subscriptions at once

## Connection steps

{% stepper %}
{% step %}
#### Go to Settings → Integrations

In your Quper workspace, navigate to **Settings → Integrations** and click **Add Integration → Azure**.
{% endstep %}

{% step %}
#### Create an App Registration

In the Azure Portal, go to **Azure Active Directory → App Registrations → New Registration**:

- Name: `Quper-ReadOnly`
- Supported account types: Accounts in this organisational directory only
- Click **Register**

Note the **Application (client) ID** and **Directory (tenant) ID** from the overview page — you will need these in step 4.
{% endstep %}

{% step %}
#### Create a client secret

On the App Registration page, go to **Certificates & Secrets → New Client Secret**:

- Description: Quper access
- Expiry: 24 months (recommended)
- Click **Add**

Copy the secret **Value** immediately — Azure will not show it again after you leave the page.
{% endstep %}

{% step %}
#### Assign the Cost Management Reader role

Go to your **Subscription → Access Control (IAM) → Add Role Assignment**:

- Role: `Cost Management Reader`
- Assign access to: User, group, or service principal
- Select: Search for your App Registration name (`Quper-ReadOnly`)
- Click **Review + Assign**

Repeat this step for each subscription you want Quper to access.
{% endstep %}

{% step %}
#### Enter credentials in Quper

Back in Quper, enter:

- **Tenant ID** — your Azure Directory (tenant) ID
- **Client ID** — your App Registration Application ID
- **Client Secret** — the secret value you copied in step 3
- **Subscription IDs** — one or more subscription IDs to connect

Click **Connect**. Quper verifies the credentials and begins initial data ingestion.
{% endstep %}
{% endstepper %}

## Connecting at Management Group level

To connect all Azure subscriptions at once, assign the `Cost Management Reader` role at the **Management Group** level instead of individual subscriptions. Quper will automatically discover and ingest data from all subscriptions under the management group.

## Troubleshooting

**"Insufficient privileges" error**
Confirm the Cost Management Reader role has been assigned to the App Registration at the subscription or management group level, not just at the resource group level.

**Data missing for some subscriptions**
If you connected individual subscriptions, make sure the role assignment was made on every subscription. Subscriptions not listed in the Quper setup will not be ingested.
