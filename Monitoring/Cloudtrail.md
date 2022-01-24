# Cloudtrail

Register by default all the actions and events happened in an AWS Account.

Log files stored in S3 are encrypted with SSE by default, but also you can select a KMS encryption.

### Log Integrity

You can view if the integrity of a Cloudtrail log file is OK using AWS CLI command:
````
aws cloudtrail validate-logs
````

### Cross Account Logging

Cross Account logging can be configured, modifying the bucket policy of destination S3, allowing the put object action from the target account.

