# Step Functions Best Practices

## Use timeouts to avoid stuck executions
By default, the Amazon States Language doesn't specify timeouts for state machine definitions. Without an explicit timeout, Step Functions often relies solely on a response from an activity worker to know that a task is complete. If something goes wrong and the TimeoutSeconds field isn't specified for an Activity or Task state, an execution is stuck waiting for a response that will never come.

To avoid this situation, specify a reasonable timeout when you create a Task in your state machine.

## Use Amazon S3 ARNs instead of passing large payloads
Executions that pass large payloads of data between states can be terminated. If the data you are passing between states might grow to over 262,144 bytes, use Amazon Simple Storage Service (Amazon S3) to store the data, and parse the Amazon Resource Name (ARN) of the bucket in the Payload parameter to get the bucket name and key value.

## Avoid reaching the history quota
AWS Step Functions has a hard quota of 25,000 entries in the execution event history. To avoid reaching this quota for long-running executions, implement a pattern that uses an AWS Lambda function that can start a new execution of your state machine to split ongoing work across multiple workflow executions.

## Handle Lambda service exceptions
AWS Lambda can occasionally experience transient service errors. In this case, invoking Lambda results in a 500 error, such as ServiceException, AWSLambdaException, or SdkClientException. As a best practice, proactively handle these exceptions in your state machine to Retry invoking your Lambda function, or to Catch the error.

## Well Choosing Standard or Express Workflows
You can choose Standard Workflows when you need long-running, durable, and auditable workflows, or Express Workflows for high-volume, event processing workloads. Your state machine executions will behave differently, depending on which Type you select. The Type you choose cannot be changed after your state machine has been created.

## Amazon CloudWatch Logs resource policy size restrictions
To avoid reaching the CloudWatch Logs resource policy size limit, prefix your CloudWatch Logs log group names with /aws/vendedlogs/. When you create a log group in the Step Functions console, the log group names are prefixed with /aws/vendedlogs/states.

---------------
[Go Home](../README.md)