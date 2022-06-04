# Autoscaling and Lifecycle Hooks

An Auto Scaling group contains a collection of Amazon EC2 instances that are treated as a logical grouping for the purposes of automatic scaling and management. An Auto Scaling group also enables you to use Amazon EC2 Auto Scaling features such as health check replacements and scaling policies. Both maintaining the number of instances in an Auto Scaling group and automatic scaling are the core functionality of the Amazon EC2 Auto Scaling service.

## By Launch Configuration
Launch configuration contains details about the EC2 instances to deploy inside an Autoscaling Group. Is not versionable.

## By Launch Template
Is and advanced way to configure EC2 instances in an ASG. It allows to choose between on demand and spot instances. It's versionable.

## Scheduled Actions
Allows to schedule autoscaling actions prevent from traffic peaks that are recurrent on time.

## Scaling Policies
Selected metrics to create scaling policies are:
- Network in
- Network out
- CPU
- Load Balancer requests per target

## ALB Integration
Need to create a Target Group and assign EC2 instances. This target group can be selected on Launch Template to associate the ASG with the Target Group of the balancer.

## Suspending process and troubleshooting
For Amazon EC2 Auto Scaling, there are two primary process types: Launch and Terminate. The Launch process adds a new Amazon EC2 instance to an Auto Scaling group, increasing its capacity. The Terminate process removes an Amazon EC2 instance from the group, decreasing its capacity.

Each process type can be suspended and resumed independently. Keep in mind that suspending individual processes might interfere with other processes. Depending on the reason for suspending a process, you might need to suspend multiple processes together.

## Lifecycle Hooks
![Lifecycle](https://docs.aws.amazon.com/autoscaling/ec2/userguide/images/auto_scaling_lifecycle.png)

Using the Pending:Wait and Pending:Proceed you can pre-configure instances with long duration processes.

Using the Terminating:Wait and Terminating:Proceed you have an use case collecting logs previously to the instance termination.

Is useful to use both integrated with Cloudwatch Events and lambda.

Lambda needs to notify to Autoscaling with an API call that it ends his workflow.

## Termination Policies
When scale in, termination policies mark what instance is deleted.

- Default: Remove the instance from the AZ with most instances.
- OldestInstance
- OldestLaunch*
- NewestInstance
- AllocationStrategy: Try to maintain the combination between spot and on demand
- ClosesToNextInstanceHour: Instances that are closer to the billing hour.

## Cloudformation Create & UpdatePolicy
Creation policies is useful to tell Cloudformation to make a rollback when the instance provisioning fails.

Update policies allow to switch the EC2 fleet inside the ASG when you apply a change in Launch Configuration/Template.
- AutoscalingReplacingUpdate
- AutoscalingRollingUpdate
Both apply only when you do a change on Launch Template/Configuration or VPC Zone Identifier of ASG. If both properties are given, setting WillReplace propertie to _true_ gives Replacing precedence.
- AutoscalingScheduledAction applies when you update an stack with an associate Scheduled Action. Is used to prevent scheduled actions from modifyin min/max/desired for cloudformation.

## Deployment Strategies
- In Place: Deploys on same instance, making it mutable.
- Rolling: Adding new instances with new version and remove olds.
- Replace: Create a new Autoscaling Group and switch the target group.
- Blue/Green: Create a new environment(ASG, TG and ASG) and switch between it.

---------------
[Go Home](../README.md)