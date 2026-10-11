# Live AWS CloudTrail and CloudWatch Labs

These exercises were completed in a personal AWS lab environment using an IAM user rather than the AWS root account.

Sensitive account identifiers, access-key information, source IP addresses, and request identifiers are redacted where appropriate.

## CloudTrail — Authorization Failure

An IAM user attempted to create an S3 bucket before the required permissions were available.

CloudTrail recorded the failed management event with:

- User identity: `cloudsupport-lab`
- Event: `CreateBucket`
- Event source: `s3.amazonaws.com`
- Error: `AccessDenied`
- Read-only: `false`

![CloudTrail AccessDenied event](screenshots/aws-cloudtrail-createbucket-access-denied.png)

This demonstrates using CloudTrail to distinguish an authorization failure from an application or service failure.

## IAM Permission Correction and Successful Retry

Permissions were managed through an IAM group. After granting the lab user the permissions required for the exercise, the S3 bucket creation was retried successfully.

CloudTrail then showed:

- User identity: `cloudsupport-lab`
- Event: `CreateBucket`
- Event source: `s3.amazonaws.com`
- No error code
- Referenced S3 resource
- Read-only: `false`

![Successful CloudTrail CreateBucket event](screenshots/aws-cloudtrail-createbucket-success.png)

This demonstrates correlating a failed operation with IAM permissions and confirming successful remediation through a subsequent CloudTrail event.

## CloudWatch Logs Insights

A CloudWatch log group was populated with sample support events and queried using Logs Insights.

The query isolated ERROR-level messages:

~~~text
fields @timestamp, @message
| filter @message like /ERROR/
| sort @timestamp desc
~~~

![CloudWatch Logs Insights error query](screenshots/aws-cloudwatch-logs-insights-errors.png)

The results identified:

- Authentication token expiration
- Database connection timeout

## Skills Demonstrated

- AWS CloudTrail event investigation
- IAM authorization troubleshooting
- IAM group-based permissions
- S3 management-event analysis
- Successful versus denied API activity
- CloudWatch log groups and streams
- CloudWatch Logs Insights
- Filtering application logs
- Timestamp-based sorting
- Cross-cloud log investigation
