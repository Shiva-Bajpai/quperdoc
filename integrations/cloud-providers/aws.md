---
description: Connect your AWS account to Quper via a read-only IAM Role.
icon: cloud
---

# Connect to AWS

Quper connects to AWS using a cross-account IAM Role with read-only permissions. This is the most secure connection method — no access keys are stored, and Quper can only read your billing and usage data.

## What Quper tracks from AWS

- All AWS service costs via the Cost and Usage Report (CUR)
- EC2 instance usage, instance types, and running hours
- RDS, Lambda, S3, EKS, and all other AWS service spend
- Reserved Instance and Savings Plan utilisation and coverage
- Cost and usage broken down by account, region, service, and tag
- Hourly spend signals for real-time anomaly detection

## Before you begin

- You must have **IAM administrator access** in the AWS account you want to connect
- Quper supports connecting **multiple AWS accounts** — repeat this process for each account, or use AWS Organizations to connect all accounts in bulk

## Connection steps

{% stepper %}
{% step %}
#### Go to Settings → Integrations

In your Quper workspace, navigate to **Settings → Integrations** and click **Add Integration → AWS**.
{% endstep %}

{% step %}
#### Deploy the IAM Role via CloudFormation

Quper provides a one-click CloudFormation template that creates the read-only IAM Role in your AWS account. Click **Launch CloudFormation Template** — this opens the AWS Console with the stack pre-configured.

Review the stack parameters and click **Create Stack**. The stack creates:

- An IAM Role named `QuperReadOnlyRole`
- A policy granting read-only access to Cost Explorer, Cost and Usage Reports, and CloudWatch
- A trust relationship allowing Quper's AWS account to assume the role
{% endstep %}

{% step %}
#### Copy the Role ARN

Once the CloudFormation stack status shows **CREATE_COMPLETE**, go to the **Outputs** tab of the stack and copy the `QuperRoleARN` value.
{% endstep %}

{% step %}
#### Paste the Role ARN into Quper

Return to the Quper integrations setup screen, paste the Role ARN, and click **Connect**. Quper will verify the role and begin initial data ingestion.
{% endstep %}
{% endstepper %}

## Connecting multiple AWS accounts

To connect additional AWS accounts, repeat the steps above for each account. Quper will display all connected accounts in a unified view in the Spend Overview, with the ability to filter by account.

If you use **AWS Organizations**, you can optionally connect the management account and grant Quper access to all member accounts at once. Contact Quper support for the Organizations setup guide.

## Permissions granted to Quper

The IAM Role created by the CloudFormation template grants the following read-only permissions:

| Service | Permissions |
|---|---|
| Cost Explorer | `ce:GetCostAndUsage`, `ce:GetReservationUtilization`, `ce:GetSavingsPlansUtilization` |
| Cost and Usage Reports | `cur:DescribeReportDefinitions` |
| S3 (CUR bucket) | `s3:GetObject`, `s3:ListBucket` |
| CloudWatch | `cloudwatch:GetMetricStatistics`, `cloudwatch:ListMetrics` |
| Organizations (optional) | `organizations:ListAccounts`, `organizations:DescribeAccount` |

Quper does not request and cannot be granted any write permissions through this role.

## Troubleshooting

**Quper shows "Role verification failed"**
Verify that the CloudFormation stack completed successfully (status: `CREATE_COMPLETE`) and that you copied the full ARN including the account ID.

**No data appearing after 30 minutes**
Ensure your AWS account has Cost and Usage Reports enabled in **Billing → Cost & Usage Reports**. If CUR is not yet set up, Quper will set up a new report — allow up to 24 hours for the first report to be delivered.

**Some services show $0 cost**
Certain AWS services report costs with a 24–48 hour delay in CUR. This is expected behaviour from AWS. Quper displays costs as soon as they are available in the report.
