# AWS Code*
## Codecommit
- Source coding control version
- Supports http, ssh and GRC

One way to secure branch master in Codecommit is create a role that can't push directly to master and assign to people.

Can use notification rules or AWS Eventbridge to handle events in the codecommit repository
## Codebuild
Fully managed build service from AWS. It compiles the code, run unit tests, produces artifacts that are ready to deploy...

- Eliminate the need to provision build servers
- Provides pre-packaged environments
- Allow custom environments (Custom docker image)
- Scales automatically
- Timeout longer than Lambda
- Output logs can be send to S3 or AWS Cloudwatch

**Buildspec file**

It's a yaml file that contains the configuration for the build. It's divided by phases.

See reference on: [Buildspec Reference](https://docs.aws.amazon.com/codebuild/latest/userguide/build-spec-ref.html)

**Build phase transitions:**

![](https://docs.aws.amazon.com/codebuild/latest/userguide/images/build-phases.png)
```
Important

The UPLOAD_ARTIFACTS phase is always attempted, even if the BUILD phase fails.
```

**Environment Variables**

AWS Codebuild has pre-defined environment variables like AWS_REGION, AWS_ACCOUNT_ID or CODEBUILD_ID

See Reference on: [Environment Variables Reference](https://docs.aws.amazon.com/codebuild/latest/userguide/build-env-ref-env-vars.html)

Also you can insert your own environment variables in the _env_ statement in buildspec, using parameter store or in Buildspec configuration.

**Artifacts**

You can upload generated artifacts to a S3. This may be configured on buildspec file.

## CodeDeploy
Managed deployment service that automates deploys to:
- EC2 -> Selected by tag (Must be running the CodeDeploy Agent) or ASG
- On-prem servers -> First register on CodeDeploy using IAM authentication (User or Role(More secure, because use STS with temporary credentials)) after it, need to tag
- Lambda functions -> 2 ways, all at once that switch version or using Canary deployment.

Also make easier:
- New Features launch
- Rollback available (Automatic, Manual)
- Automatic rollback triggers when fail or AWS Cloudwatch Alarm
- Avoid downtime during deployments
- Handle full process without human intervention

**Steps:**

Source code + appspec file ->  Upload to Github or S3 -> Trigger Deployment -> Agent Poll for what to do -> Download appspec and source code in target.

Codedeploy works following this steps:
You must create a DeploymentGroup with target instances and after that launch a deployment to this deployment group.

**Appspec file** **(TOO MUCH IMPORTANT)**

It marks the hooks inside the deployment action. 

See reference on: [Appspec Reference](https://docs.aws.amazon.com/codedeploy/latest/userguide/reference-appspec-file.html)

Hooks are predefined by AWS and each hook is executed in an exact time slot.
In reference you can see all the cases availables depending on your deployment type.
Hooks also has environment variables.

See reference on: [Hooks Reference](https://docs.aws.amazon.com/codedeploy/latest/userguide/reference-appspec-file-structure-hooks.html)


## Codepipeline

Orchestrate all CI/CD Logic.

- Each pipeline stage can create Artifacts
- Artifacts are passed stored in S3 and passed to the next stage

*Source Stage:*

Can be triggered by Codecommit, Github, S3 or ECR. Change detection options is an Event or Poll for changes.
If use SCM, you need to manage a pipeline for only 1 branch, so multibranching is not possible.

---

After source stage you need to create actions that can be Deploy, Build, Invoke, Manual Approve... etc

You can create Invoke action jobs using AWS Lambda to manage actions that predefined actions by CodePipeline can't do, like update DNS as example.

Also, AWS CodePipeline includes a number of actions that help you configure build, test, and deploy resources for your automated release process. If your release process includes activities that are not included in the default actions, such as an internally developed build process or a test suite, you can create a custom action for that purpose and include it in your pipeline. You can use the AWS CLI to create custom actions in pipelines associated with your AWS account.

You can create custom actions for the following AWS CodePipeline action categories:

- A custom build action that builds or transforms the items
- A custom deploy action that deploys items to one or more servers, websites, or repositories
- A custom test action that configures and runs automated tests
- A custom invoke action that runs functions

When you create a custom action, you must also create a job worker that will poll CodePipeline for job requests for this custom action, execute the job, and return the status result to CodePipeline. This job worker can be located on any computer or resource as long as it has access to the public endpoint for CodePipeline. To easily manage access and security, consider hosting your job worker on an Amazon EC2 instance.
The following diagram shows a high-level view of a pipeline that includes a custom build action:

![Diagram](https://docs.aws.amazon.com/codepipeline/latest/userguide/images/PipelineCustomActionCS.png)

Recommended lecture: [Codepipeline Blog](https://aws.amazon.com/blogs/devops/implementing-gitflow-using-aws-codepipeline-aws-codecommit-aws-codebuild-and-aws-codedeploy/)


# CodeStar

Integrated environment in that you quickly develop your application projects.

---------------
[Go Home](../README.md)