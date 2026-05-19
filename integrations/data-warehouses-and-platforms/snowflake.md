---
description: Connect your Snowflake account to Quper to track warehouse credits and query costs.
icon: database
---

# Connect to Snowflake

Quper connects to Snowflake using a dedicated read-only user and role. It tracks warehouse credit consumption, query costs, storage spend, and idle compute — giving you full visibility into where your Snowflake spend is going and which teams or workloads are driving it.

## What Quper tracks from Snowflake

- Warehouse credit consumption by warehouse, user, and query type
- Storage costs including data storage, failsafe, and stage storage
- Query-level cost attribution — spend per query, role, user, and database
- Idle warehouse time and auto-suspend performance
- Credit usage trends and anomalies in real time

## Before you begin

- You must have **ACCOUNTADMIN** access to create the Quper user and role
- Quper supports connecting **multiple Snowflake accounts** — repeat this process for each account

## Connection steps

{% stepper %}
{% step %}
#### Go to Settings → Integrations

In your Quper workspace, navigate to **Settings → Integrations** and click **Add Integration → Snowflake**.
{% endstep %}

{% step %}
#### Run the setup SQL in Snowflake

Quper provides a ready-to-run SQL script that creates a dedicated user and role with read-only access. Run the following in a Snowflake worksheet as ACCOUNTADMIN:

```sql
-- Create Quper role
CREATE ROLE IF NOT EXISTS QUPER_READER;

-- Grant access to billing and usage views
GRANT IMPORTED PRIVILEGES ON DATABASE SNOWFLAKE TO ROLE QUPER_READER;

-- Create Quper user
CREATE USER IF NOT EXISTS QUPER_SERVICE_USER
  PASSWORD = '<generate-a-strong-password>'
  DEFAULT_ROLE = QUPER_READER
  DEFAULT_WAREHOUSE = '<your-warehouse>'
  MUST_CHANGE_PASSWORD = FALSE;

-- Assign role to user
GRANT ROLE QUPER_READER TO USER QUPER_SERVICE_USER;
```

Replace `<generate-a-strong-password>` with a strong password and `<your-warehouse>` with any warehouse that can run lightweight queries.
{% endstep %}

{% step %}
#### Enter credentials in Quper

Back in Quper, enter:

- **Account Identifier** — your Snowflake account locator (e.g. `xy12345.us-east-1`)
- **Username** — `QUPER_SERVICE_USER`
- **Password** — the password you set in the SQL above
- **Warehouse** — the warehouse name you specified

Click **Connect**. Quper verifies the connection and begins ingesting usage and billing data.
{% endstep %}
{% endstepper %}

## What queries Quper runs

Quper queries the `SNOWFLAKE.ACCOUNT_USAGE` schema to pull billing and usage data. These queries are read-only and run once per hour on a small warehouse. Quper's query load on your Snowflake account is minimal — typically less than 1 credit per day.

## Troubleshooting

**"Insufficient privileges" error**
Confirm that `IMPORTED PRIVILEGES` was granted on the `SNOWFLAKE` database to the `QUPER_READER` role. This is the specific grant that enables access to `ACCOUNT_USAGE` views.

**Data has a 45-minute delay**
This is expected. Snowflake's `ACCOUNT_USAGE` views have a built-in latency of up to 45 minutes. Quper reflects this accurately in its ingestion timestamps.
