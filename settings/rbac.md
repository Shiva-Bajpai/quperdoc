---
description: Control who can see what in Quper with role-based access and team-level data scoping.
icon: users
---

# Role-Based Access Control (RBAC)

Quper's RBAC system lets you control what each user can do and which cost data they can see. Access is managed through two layers: **roles** (what actions a user can take) and **teams** (which data a user can see).

## Default roles

Quper ships with three built-in roles that cover most use cases:

| Role | Capabilities |
|---|---|
| **Admin** | Full access to all settings, integrations, users, billing data, governance policies, and optimisation actions |
| **Editor** | Can view all cost data, create and edit dashboards, configure budgets, apply recommendations, and manage alerts. Cannot manage users or integrations |
| **Viewer** | Read-only access to dashboards, cost data, anomaly alerts, and reports. Cannot apply changes or modify any configuration |

## Custom roles

If the default roles don't fit your organisational structure, you can create custom roles with granular permission controls.

### Creating a custom role

1. Go to **Settings → Users & Access → Roles**
2. Click **Create Role**
3. Enter a role name and optional description
4. Toggle individual permissions on or off (see the permissions list below)
5. Click **Save Role**

### Permissions list

| Permission | Description |
|---|---|
| `integrations.view` | View connected integrations and their status |
| `integrations.manage` | Add, disconnect, and reconfigure integrations |
| `spend.view` | View Spend Overview and cost breakdowns |
| `anomalies.view` | View anomaly alerts and their details |
| `anomalies.manage` | Comment on, dismiss, and mark anomalies as expected |
| `recommendations.view` | View Action Intelligence recommendations |
| `recommendations.apply` | Apply one-click optimisation actions |
| `governance.view` | View governance score, budgets, and tag policies |
| `governance.manage` | Create and edit budgets, tag policies, and team ownership rules |
| `reports.view` | View and download governance and spend reports |
| `reports.schedule` | Create and manage scheduled report delivery |
| `users.view` | View the user list and their roles |
| `users.manage` | Invite users, assign roles, and remove users |
| `settings.view` | View account settings |
| `settings.manage` | Modify account settings, security configuration, and workspace preferences |

## Teams and data access scoping

Teams allow you to restrict what cost data a user sees. Users assigned to a team only see cost data attributed to that team's resources — they cannot see company-wide spend or data from other teams.

This is useful for:
- Giving individual engineering squads visibility into their own cloud spend without exposing company billing data
- Providing cost ownership to team leads without granting company-wide Admin access
- Compliance requirements where finance data must be restricted to specific personnel

### Creating a team

1. Go to **Settings → Users & Access → Teams**
2. Click **Create Team**
3. Enter a team name
4. Define the team's attribution rules — the resource tags that map spend to this team (e.g. `team:data-engineering`)
5. Add team members and assign their roles within the team context
6. Set team-specific budgets and notification preferences (optional)

### How data scoping works

When a user is a member of a team with data scoping enabled, Quper filters all cost data to show only resources that match the team's attribution rules. This applies to:

- Spend Overview
- Anomalies feed
- Action Intelligence recommendations
- Governance dashboards and reports

Users can be members of multiple teams. If a user belongs to multiple teams, they see the combined data from all their teams.

## Managing users

### Inviting a user
1. Go to **Settings → Users & Access → Users**
2. Click **Invite User**
3. Enter the user's email address
4. Select their role
5. Optionally assign them to one or more teams
6. Click **Send Invite**

The invitation email expires after **48 hours**. Resend it from the Users list if needed.

### Editing a user's role
1. In the Users list, click the options menu (⋯) next to the user
2. Select **Edit Role**
3. Choose the new role and click **Save**

### Removing a user
1. In the Users list, click the options menu (⋯) next to the user
2. Select **Remove User**
3. Confirm the removal

Removed users immediately lose access to the workspace. Their historical activity (comments, applied recommendations) is retained in the audit log.

## RBAC FAQs

**Can an Admin lock themselves out of the workspace?**
No. Quper prevents the last Admin user from being downgraded or removed. At least one Admin must exist in every workspace at all times.

**What happens if I remove a user who owns budgets or governance policies?**
Budget and policy ownership is transferred to the Admin who performed the removal. Quper notifies that Admin so they can reassign ownership.

**Can I use SSO groups to automatically assign Quper roles?**
Yes. When configuring SAML SSO, you can map identity provider group attributes to Quper roles. Users are automatically assigned the correct role when they sign in through SSO. See [Account Settings](account.md) for SSO configuration.
