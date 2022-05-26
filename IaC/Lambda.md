# Lambda

Lambda is a compute service that lets you run code without provisioning or managing servers. Lambda runs your code on a high-availability compute infrastructure and performs all of the administration of the compute resources, including server and operating system maintenance, capacity provisioning and automatic scaling, code monitoring and logging. With Lambda, you can run code for virtually any type of application or backend service.

### Sources & Use Cases

Lambda can be triggered by many services, as example:

**API Gateway**
allows to create an external API and receive calls

**Application Load Balancer**
Also like API Gateway but more weak configuration options

**Cloudwatch Events**

All of the events occured in AWS can launch a lambda function, so this open many posibilities to be a source of lambda.

**Cloudwatch Logs**
**DynamoDB**
**Kinesis**
**S3**
**SNS&SQS**

and external sources like DataDog.

### Security and Environment Variables

Lambda has environment variables that can be loaded in the code at runtime.
This variables also may be encripted using KMS Customer Managed Keys.
Encrypted variables needs to be desencrypted using Boto3 KMS client in the code.
Also you can use SSM Parameter Store or Secrets Manager to handle your variables.

### Versions, Aliases and Canary Routing

When you work on a Lambda function, usually work on $LATEST version.
When we publish to lambda, we create a version. Versions are INMUTABLE and never change.

Aliases are pointers to Lambda function versions. We can define a dev, test or prod aliases to different verions. 
Aliases are mutable and can be pointed to a specific version, or use $LATEST version.
Aliases enable Blue/Green Canary deployment by assigning weights to lambda functions.

### SAM Framework

Serverless Application Model is a CLI to easily create and manage lambda applications as code.

*sam init* command is used to manage scaffolding of a SAM project. It creates the SAM template and the base function code.

SAM uses cloudformation code with a little peculiarities.

*sam build* command build dependencies and create an .aws-sam folder with all the necessary.

You can test locally the lambda using Docker with the *sam local invoke* and *s*am local start-api* commands.

With *sam package* you can package all the builded project of sam and upload to a S3 bucket ready to deploy.

Finally to deploy it use the *sam deploy* command.

If you are using SAM, it comes built-in with CodeDeploy to deploy lambda versions.

You can deploy versions and create aliases that point to specific version.

## Step Functions

### Use Cases

Step Functions are used with very complex workflow and need to isolate to make it more visual.

It's very integrable with batch Jobs using AWS Batch.

AWS Step Functions are based on state machines.

See more on: [Step functions use cases](https://aws.amazon.com/es/step-functions/use-cases/)

---------------
[Go Home](../README.md)