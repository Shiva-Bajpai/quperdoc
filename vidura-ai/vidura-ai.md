---
description: Quper's AI engine for root cause analysis, anomaly detection, and cost optimisation.
icon: sparkles
---

# Vidura AI

Vidura is Quper's built-in AI engine. It monitors hundreds of signals across your cloud infrastructure in real time, performs root cause analysis on cost events, and generates ranked optimisation recommendations — so your team always knows what is happening and what to do about it.

Vidura is not a chatbot layered on top of your data. It is the intelligence layer that powers everything Quper does: every anomaly alert, every recommendation, and every root cause explanation comes from Vidura's analysis.

## What Vidura does

### Real-time monitoring
Vidura continuously ingests usage and billing signals from all connected cloud providers and data platforms. It processes these signals against learned baselines to detect deviations the moment they occur — not hours or days later.

### Anomaly detection
Vidura's ML models build a baseline of expected behaviour for every service, account, region, and resource in your environment. When usage deviates from this baseline, Vidura generates an alert with:

- The specific resource and service causing the anomaly
- The magnitude of the deviation (e.g. 3.4× normal usage rate)
- The per-hour cost impact
- A projected end-of-day cost if left unresolved

### Root cause analysis
Every anomaly Vidura detects comes with an explanation in plain language. Vidura identifies what changed — a new resource launched without auto-stop, a query pattern that changed, a warehouse that stopped auto-suspending — and surfaces it alongside the alert so your team can act without manual investigation.

### Optimisation recommendations
Vidura continuously scans your infrastructure for rightsizing opportunities, idle resources, missing configurations, and commitment gaps. Recommendations are ranked by monthly savings potential and include:

- The specific action to take
- The estimated monthly savings
- A confidence level based on how long the pattern has been observed
- One-click application for supported platforms

### Forecast and run rate
Vidura projects your end-of-month spend based on current usage trajectory. If a cost anomaly is active, Vidura shows a separate "if unresolved" forecast so you can quantify the impact of inaction.

## How Vidura surfaces its analysis

Vidura's outputs appear throughout the Quper interface:

| Where | What Vidura shows |
|---|---|
| **Spend Overview** | Run rate forecast, anomaly markers on the spend chart |
| **Anomalies feed** | Detected anomalies with root cause explanations |
| **Action Intelligence** | Ranked optimisation recommendations with savings estimates |
| **Governance dashboard** | Policy compliance analysis and gap identification |
| **Integration setup** | Initial analysis and first recommendations on data ingestion |

## Vidura's learning period

Vidura requires a minimum of **14 days of usage data** to establish reliable baselines for anomaly detection. During this period:

- Spend Overview and recommendations are available immediately
- Anomaly detection operates at reduced sensitivity with a wider deviation threshold
- After 14 days, sensitivity increases and false positive rates decrease significantly

Vidura continues to improve its baselines over time as it observes more of your infrastructure's behaviour patterns.

## Data privacy and security

Vidura's analysis runs entirely within Quper's secure infrastructure. Your billing and usage data is never shared with third-party AI providers or used to train models outside of your workspace. Vidura's models are trained on your organisation's own cost and usage patterns only.

Quper is SOC 2 Type II certified. All data is encrypted in transit and at rest.

## FAQs

**Does Vidura have access to my actual workloads or data?**
No. Vidura only analyses billing and usage metadata — the same data you see in your cloud provider's billing console. It has no access to the contents of your databases, code, or application data.

**Can Vidura make changes to my cloud resources automatically?**
Vidura can apply approved optimisations with one-click confirmation in Quper. It does not make autonomous changes to your infrastructure without explicit approval. All actions are logged in the Decision Trail.

**How does Vidura compare to my cloud provider's native cost tools?**
Native tools (AWS Cost Explorer, GCP Cost Management, Azure Cost Analysis) show you what happened. Vidura explains why it happened and what to do about it — across all your providers in a single place.
