---
description: Manage your Quper workspace settings, billing, and security configuration.
icon: gear
---

# Account Settings

Account Settings is where you configure your Quper workspace — your organisation profile, security settings, billing, and workspace-wide preferences.

## Accessing Account Settings

Navigate to **Settings → Account** from the left sidebar. Only users with the **Admin** role can view and modify account settings.

## Workspace profile

- **Workspace name** — the display name for your organisation in Quper
- **Workspace slug** — the URL-friendly identifier used in API calls and exports
- **Time zone** — the default time zone used for cost reporting, budget periods, and scheduled reports
- **Fiscal year start** — the month your financial year begins, used to align budget periods and financial reports

## Security

### Single Sign-On (SSO)
Configure SAML 2.0 SSO to require all users to authenticate through your identity provider. See the [Onboarding](../getting-started/onboarding.md) guide for setup instructions.

### Session management
- **Session timeout** — set how long inactive sessions remain valid (default: 8 hours, maximum: 30 days)
- **Force re-authentication** — require users to re-authenticate before applying optimisation actions

### IP Allowlist
Restrict Quper access to specific IP addresses or CIDR ranges. When enabled, users outside the allowed IPs cannot log in or access the Quper API.

To enable:
1. Go to **Settings → Account → Security → IP Allowlist**
2. Click **Add IP Range** and enter the CIDR notation (e.g. `203.0.113.0/24`)
3. Add all required ranges including your office IPs and VPN exit nodes
4. Click **Enable Allowlist**

{% hint style="info" %}
Before enabling the IP Allowlist, ensure your own IP is in the allowlist. Enabling it without including your current IP will lock you out of the workspace.
{% endhint %}

## Data retention

Quper retains your cloud cost and usage data for **24 months** by default. You can configure a shorter retention period if required for compliance.

Raw billing data from connected integrations is retained separately in your cloud provider's billing systems — Quper does not store a copy of the raw data.

## Workspace deletion

To delete your Quper workspace, contact [support@quper.co](mailto:support@quper.co). Workspace deletion is irreversible and permanently removes all cost data, configurations, and user accounts associated with your workspace.
