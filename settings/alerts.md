---
description: Configure where Quper sends cost anomaly alerts, budget notifications, and governance reports.
icon: bell
---

# Alerts & Notifications

Quper sends notifications for cost anomalies, budget breaches, governance policy violations, and scheduled reports. You can configure where these alerts go — email, Slack, Microsoft Teams, or a custom webhook.

## Notification channels

### Email
Email notifications are enabled by default for all users. Each user receives alerts for events relevant to their role and team.

To configure email preferences:
1. Go to **Settings → Notifications → Email**
2. Select which event types you want to receive email notifications for
3. Set the digest frequency — immediate, daily digest, or weekly digest

### Slack

Connect Quper to your Slack workspace to receive real-time cost alerts in any channel.

**Setup:**
1. Go to **Settings → Notifications → Slack**
2. Click **Connect Slack**
3. Authorise the Quper Slack app in your workspace
4. Select the default channel for Quper notifications
5. Click **Save**

You can configure different alert types to route to different channels — for example, Critical anomalies to `#incidents` and weekly governance reports to `#finops`.

### Microsoft Teams

Connect Quper to Microsoft Teams to receive alerts in any Teams channel.

**Setup:**
1. Go to **Settings → Notifications → Microsoft Teams**
2. Click **Add Webhook**
3. In Microsoft Teams, go to your target channel → **Connectors → Incoming Webhook**
4. Create a new webhook and copy the webhook URL
5. Paste the URL into Quper and click **Save**

### Custom Webhook

Send Quper notifications to any endpoint that accepts HTTP POST requests — useful for integrating with PagerDuty, OpsGenie, Jira, or your own internal systems.

**Setup:**
1. Go to **Settings → Notifications → Webhooks**
2. Click **Add Webhook**
3. Enter your endpoint URL
4. Select the event types to send to this endpoint
5. Optionally add authentication headers
6. Click **Test Webhook** to verify the connection, then **Save**

Quper sends webhook payloads as JSON. The payload schema is documented in the API reference.

## Notification event types

Configure which events trigger notifications and at what severity level:

| Event | Description |
|---|---|
| **Anomaly detected** | A new cost anomaly has been detected (configurable by severity: Critical, High, Medium, Low) |
| **Anomaly resolved** | A previously detected anomaly has returned to baseline |
| **Budget threshold reached** | Spend has crossed a configured budget alert threshold (e.g. 70%, 90%, 100%) |
| **Budget exceeded** | Spend has exceeded the budget cap for the period |
| **Tag policy violation** | A new untagged resource was detected that violates a governance policy |
| **Governance report** | Weekly governance score and compliance summary |
| **Recommendation available** | Vidura AI has surfaced a new high-impact recommendation (configurable by savings threshold) |

## Alert routing rules

You can route different notification types to different channels. For example:

- Critical and High anomalies → Slack `#finops-alerts` + PagerDuty webhook
- Budget threshold alerts → Email to budget owners
- Weekly governance report → Slack `#finops` + email to finance stakeholders
- New recommendations over $1,000/mo savings → Email to FinOps lead

To configure routing rules:
1. Go to **Settings → Notifications → Routing Rules**
2. Click **Create Rule**
3. Select the event type and severity filter
4. Choose the destination channel
5. Optionally filter by team, cloud provider, or spend threshold
6. Click **Save**

## Notification limits

- Quper will not send more than **1 notification per anomaly per hour** to prevent alert fatigue during active incidents
- Budget threshold alerts are sent once per threshold crossing — you will not receive repeated alerts at the same threshold level until the next budget period
- A maximum of **10 webhook endpoints** can be configured per workspace

## FAQs

**Can I snooze alerts for a specific resource?**
Yes. From any anomaly alert, click **Snooze** to suppress notifications for that resource for a defined period (1 hour, 4 hours, 24 hours, or 7 days). The anomaly remains visible in the Anomalies feed — only notifications are suppressed.

**Can different team members receive different alerts?**
Yes. Each user can configure their personal notification preferences in **Profile → Notifications**. Workspace-wide routing rules set by Admins are applied in addition to personal preferences.

**How do I notify a specific person when their team's budget is breached?**
Assign budget owners when creating a budget in **Govern → Cost Governance → Budgets**. Budget owners receive notifications automatically when their budget thresholds are crossed, regardless of their general notification settings.
