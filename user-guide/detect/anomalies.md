---
description: Detect abnormal cost patterns the moment they emerge — with full root-cause context.
icon: bell-alert
---

# Anomalies

Quper detects abnormal cost and usage patterns across all your connected cloud providers and data platforms in real time. Every anomaly alert comes with the full context of what changed, which workload is responsible, and what it is costing per hour — so your team can act immediately instead of waiting for the monthly bill.

## How anomaly detection works

Quper's ML-powered detection engine builds a baseline of expected spend for every service, account, region, and resource combination. It continuously monitors incoming usage signals against this baseline and flags deviations that exceed statistical thresholds.

Detection happens at two levels:

- **Spend anomalies** — unexpected spikes or drops in cost for a service or resource
- **Usage anomalies** — unexpected changes in resource consumption patterns (e.g. a warehouse running continuously when it normally auto-suspends)

Alerts are generated in real time as anomalies are detected — not on a daily schedule.

## The Anomalies feed

Navigate to **Detect → Anomalies** to see all active and historical anomaly alerts.

Each anomaly in the feed shows:

- **Service and resource** — the specific cloud service and resource driving the anomaly
- **Severity** — Critical, High, Medium, or Low based on cost impact and deviation magnitude
- **Current usage rate** — the per-hour cost at the time of detection
- **Baseline rate** — the normal expected cost for this resource
- **Deviation** — how much the current rate exceeds the baseline (e.g. 3.4× normal)
- **Running since** — when the anomaly started
- **EOD forecast** — projected end-of-day cost if the anomaly is not resolved
- **Root cause** — Vidura AI's explanation of what changed and why

## Anomaly severity levels

| Severity | Criteria |
|---|---|
| **Critical** | Spend is more than 5× baseline or exceeds $1,000/hr deviation |
| **High** | Spend is 3–5× baseline or exceeds $500/hr deviation |
| **Medium** | Spend is 2–3× baseline or exceeds $100/hr deviation |
| **Low** | Spend is 1.5–2× baseline — informational, worth monitoring |

## Responding to an anomaly

Click any anomaly in the feed to open the detail view. From here you can:

1. **Review the root cause** — Vidura AI explains what triggered the anomaly (e.g. "A new EC2 instance was launched in us-east-1 without auto-stop configured and has been running for 2h 14m")
2. **See the affected resource** — drill into the specific instance, cluster, warehouse, or job driving the spike
3. **Apply a recommendation** — if Quper has an automated fix available (e.g. terminate idle instance, resize warehouse), you can apply it with one click
4. **Add a comment** — document why the anomaly occurred for your team's audit trail
5. **Mark as expected** — if the spike is intentional (e.g. a planned data migration), mark it as expected to suppress future alerts for this pattern

## Configuring alerts

By default, all Critical and High severity anomalies trigger notifications. You can configure where Quper sends alerts in **Settings → Alerts & Notifications**.

Supported notification channels:
- Email
- Slack
- Microsoft Teams
- Webhook (for custom integrations)

You can set notification rules by severity level, cloud provider, team, or spend threshold.

## Limitations

- Anomaly detection requires at least **14 days of historical data** to establish a reliable baseline. During the first 14 days after connecting an integration, detection sensitivity is lower.
- A maximum of **150 active anomaly alerts** are displayed in the feed at one time. Alerts are prioritised by cost impact.
- Usage anomalies for Snowflake and Databricks have a maximum latency of **45–60 minutes** due to upstream data availability in those platforms.

## FAQs

**Why am I seeing anomalies on my first day?**
Quper backfills 90 days of historical data when you connect an integration. It uses this history to build an initial baseline and immediately flags any resources that have been behaving abnormally in your historical data.

**How do I reduce false positives?**
Mark recurring intentional spikes as "expected" patterns. After 3 or more occurrences, Quper learns this is a recurring event and adjusts the baseline accordingly.

**Can I set custom thresholds?**
Yes. In **Settings → Alerts & Notifications**, you can configure custom alert thresholds per service or team, overriding Quper's default severity classification.
