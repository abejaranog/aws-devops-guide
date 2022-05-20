# AWS Config
Provides an audit trail of resources and rules to accomplish by them.

The configuration history is saved in S3 buckets. Also you can be notified using SNS.

Once installed, Config has an inventory of AWS resources and you can view a configuration timeline on each resource.

## Rules
AWS Config provides AWS managed rules, which are predefined, customizable rules that AWS Config uses to evaluate whether your AWS resources comply with common best practices. For example, you could use a managed rule to quickly start assessing whether your Amazon Elastic Block Store (Amazon EBS) volumes are encrypted or whether specific tags are applied to your resources. You can set up and activate these rules without writing the code to create an AWS Lambda function, which is required if you want to create custom rules.

After you activate a rule, AWS Config compares your resources to the conditions of the rule. After this initial evaluation, AWS Config continues to run evaluations each time one is triggered. The evaluation triggers are defined as part of the rule, and they can include the following types:

- Configuration changes – AWS Config triggers the evaluation when any resource that matches the rule's scope changes in configuration. The evaluation runs after AWS Config sends a configuration item change notification.

- Periodic – AWS Config runs evaluations for the rule at a frequency that you choose (for example, every 24 hours).

## Multi Account
An aggregator is an AWS Config resource type that collects AWS Config configuration and compliance data from the following:

- Multiple accounts and multiple regions.

- Single account and multiple regions.

- An organization in AWS Organizations and all the accounts in that organization which have AWS Config enabled.

Use an aggregator to view the resource configuration and compliance data recorded in AWS Config.

Aggregators provide a read-only view into the source accounts and regions that the aggregator is authorized to view. Aggregators do not provide mutating access into the source account or region. For example, this means that you cannot deploy rules through an aggregator or pull snapshot files from the source account or region through an aggregator.