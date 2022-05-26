# AWS System Manager

Helps you manage your EC2 and On premise systems at scale.
Get operational insights about the state of your infrastructure.
Easily detect problems.
Patching automation for enhanced compliance.
Integrated with Cloudwatch and Config.

Features:
- Resource Groups
- Insights
- Parameter Store
- Actions
  -  Automation
  -  Session Manager
  -  Patch manager
  -  Maintenance Windows
  -  Run Command
  -  State Manager

### How works?

We need to install the ssm agent onto the systems we control.
Installed by default in Amazon Linux.

## Resource Groups

Are a way to group resources based on Tags or Cloudformation Stack.

## Run Command

Run command service allows to run command on the remote hosts registered on SSM. Commands are inside of Documents owned by amazon or custom.

You can select targets by tags, manually or using Resource Groups.

Also you can configure error ignoring, concurrency and send the output logs to an S3.

## Parameter Store

Is a common global storage for parameters that are retrievables using AWS CLI. Is useful to save large URLS or Config JSON files to import it later on our EC2 instances. Data also can be encrypted using KMS to save sensitive data, but is recomendable to use Secrets Manager because is a service dedicated exclusively to save secrets.

## Patch Manager

Create schedules to patch your instances.

Setting a default patch means that it will be used when patching all the Amazon Linux 2 instances in your fleet that are not associated with a patch group.

By default Amazon takes patches from itself, but you can charge your own patches to tell Patch Manager to use it.

To apply a patch manager baseline you need to create a Maintenance Window and register a target. After that, associate this maintenance window with a Run Command "RunPatchBaseline" type to execute it in the window.

## Inventory
Is used to list all instances. Also can be grouped by tag.

## Automations
Simplifies common maintenance and deployment tasks of EC2 instances and other AWS resources. Automation enables you to do the following:
- Build automation workflows to configure instances
- Create custom workflows
- Receive notifications about Automation tasks
- Monitor automatino progress and execution details.

**Example use cases:**
- Use AWS-StopEC2Instance document to automatically stop instances on a scheduling using Events.

## Session Manager
You can connect to EC2 instances on inventory using SSM-Agent and ssm-start session command.
Is useful beacause all logins has a log register on SSM Console and you can view who log in to some EC2 instance.

---------------
[Go Home](../README.md)