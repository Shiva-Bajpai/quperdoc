---
description: Connect your first cloud provider and see spend data in under 10 minutes.
icon: bolt
---

# Quickstart

This quickstart gets you connected to Quper as fast as possible. You will have live spend data and your first AI recommendations before you finish your coffee.

{% hint style="success" %}
**Estimated time: 10 minutes.** All you need is a Quper account and admin access to at least one cloud provider or data platform.
{% endhint %}

## Steps

{% stepper %}
{% step %}
#### Sign in to Quper

Log in to your Quper workspace using your credentials or your company's SSO provider. If you don't have an account yet, [book a demo](https://quper.co) to get access.
{% endstep %}

{% step %}
#### Connect your first integration

From the left sidebar, go to **Settings → Integrations** and select your cloud provider or data platform.

{% tabs %}
{% tab title="AWS" %}
Quper connects to AWS via an IAM Role. Click **Connect AWS**, then follow the CloudFormation template link to create a read-only IAM role in your account. Paste the Role ARN back into Quper to complete the connection.
{% endtab %}

{% tab title="GCP" %}
Quper connects to GCP via a Service Account. Click **Connect GCP**, download the provided setup script, and run it in your Google Cloud Shell. The script creates a service account with Billing Viewer permissions and returns a credentials JSON to paste into Quper.
{% endtab %}

{% tab title="Azure" %}
Quper connects to Azure via App Registration. Click **Connect Azure**, follow the guided App Registration steps in the Azure Portal, and paste your Tenant ID, Client ID, and Client Secret into Quper.
{% endtab %}

{% tab title="Snowflake" %}
Quper connects to Snowflake via a dedicated read-only user. Click **Connect Snowflake**, run the provided SQL commands in your Snowflake console to create the user and role, and paste your account identifier and credentials into Quper.
{% endtab %}

{% tab title="Databricks" %}
Quper connects to Databricks via a Personal Access Token. Click **Connect Databricks**, generate a token in your Databricks workspace under **User Settings → Access Tokens**, and paste it into Quper along with your workspace URL.
{% endtab %}

{% tab title="BigQuery" %}
Quper connects to BigQuery via a Service Account. Click **Connect BigQuery**, create a service account in Google Cloud IAM with BigQuery Data Viewer and Job User roles, download the key JSON, and upload it to Quper.
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Quper uses **read-only access only**. No write permissions are ever requested or required.
{% endhint %}
{% endstep %}

{% step %}
#### Wait for initial data ingestion

After connecting, Quper begins pulling your billing and usage data. Initial ingestion takes **15–30 minutes** depending on account size and how much historical data is available.

You will see a progress indicator in the Integrations panel while ingestion is running. Quper automatically pulls the last 90 days of historical data on first connection.
{% endstep %}

{% step %}
#### Explore your Spend Overview

Once data is ready, navigate to **Observe → Spend Overview**. You will see:

- Total spend this week vs. last week
- Spend breakdown by service, account, and region
- Top services by cost
- Any anomalies detected during initial ingestion

{% hint style="info" %}
If Quper detected cost anomalies in your historical data, they will appear in the **Detect → Anomalies** feed immediately.
{% endhint %}
{% endstep %}

{% step %}
#### Review Vidura AI recommendations

Go to **Decide → Action Intelligence** to see your first set of AI-generated optimisation recommendations. Each recommendation shows:

- The resource and the issue
- Estimated monthly savings
- One-click action to apply the fix

Start with the highest-impact items at the top of the list.
{% endstep %}
{% endstepper %}

## What's next?

{% content-ref url="onboarding.md" %}
[onboarding.md](onboarding.md)
{% endcontent-ref %}

{% content-ref url="../integrations/integrations.md" %}
[integrations.md](../integrations/integrations.md)
{% endcontent-ref %}

{% content-ref url="../user-guide/govern/cost-governance.md" %}
[cost-governance.md](../user-guide/govern/cost-governance.md)
{% endcontent-ref %}
