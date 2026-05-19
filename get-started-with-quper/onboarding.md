---
description: Invite your team and configure access controls for your Quper workspace.
icon: user-group
---

# Onboarding Your Team

Quper is built for collaboration across FinOps, DataOps, platform engineering, and finance teams. This guide covers how to invite users, assign roles, and set up access controls so every team member sees exactly what they need.

## Inviting users

{% stepper %}
{% step %}
#### Go to Settings → Users

From the left sidebar, navigate to **Settings → Users & Access**. Click **Invite User**.
{% endstep %}

{% step %}
#### Enter the user's email

Type the email address of the person you want to invite. Quper will send them an invitation link that expires after 48 hours.
{% endstep %}

{% step %}
#### Assign a role

Select a role for the new user. Quper ships with three default roles:

| Role | What they can do |
|---|---|
| **Admin** | Full access to all settings, integrations, billing data, and user management |
| **Editor** | Can view all cost data, create dashboards, set budgets, and apply recommendations |
| **Viewer** | Read-only access to cost data, dashboards, and reports |

You can also create custom roles with granular permissions. See [Role-Based Access Control](../settings/rbac.md) for details.
{% endstep %}

{% step %}
#### Set data access scope (optional)

If you want to restrict what cost data this user can see, assign them to a **Team** in Settings → Teams. Users in a team only see cost data that is tagged or attributed to that team's resources.

This is useful for giving engineering teams visibility into their own spend without exposing company-wide billing data.
{% endstep %}
{% endstepper %}

{% hint style="info" %}
Only **Admin** users can invite new members, manage roles, and configure integrations.
{% endhint %}

## Setting up Single Sign-On (SSO)

Quper supports SSO via SAML 2.0. To enable SSO for your workspace:

1. Go to **Settings → Security → Single Sign-On**
2. Select your identity provider (Okta, Azure AD, Google Workspace, or custom SAML)
3. Enter your IdP metadata URL or upload the metadata XML
4. Map your IdP group attributes to Quper roles
5. Test the connection, then enable SSO enforcement for your domain

{% hint style="info" %}
Once SSO enforcement is enabled, all users with your company domain must sign in through your identity provider. Password-based login is disabled for those users.
{% endhint %}

## Recommended onboarding order

For most teams, we recommend this order when setting up Quper for the first time:

1. **Connect integrations** — Get all cloud providers and data platforms connected before inviting the wider team
2. **Invite FinOps lead or admin** — This person configures budgets, tags, and governance policies
3. **Invite platform/engineering leads** — Give them Editor access so they can view anomalies and apply recommendations for their services
4. **Invite finance stakeholders** — Viewer access is typically sufficient for finance teams reviewing spend reports
5. **Invite the wider team** — Use team-scoped access to give individual squads visibility into their own spend

## What's next?

{% content-ref url="../integrations/integrations.md" %}
[integrations.md](../integrations/integrations.md)
{% endcontent-ref %}

{% content-ref url="../settings/rbac.md" %}
[rbac.md](../settings/rbac.md)
{% endcontent-ref %}

{% content-ref url="../settings/alerts.md" %}
[alerts.md](../settings/alerts.md)
{% endcontent-ref %}
