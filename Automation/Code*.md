# AWS Code*

## Codecommit
- Source coding control version
- Supports http, ssh and GRC

## Codebuild
Fully managed build service from AWS. It compiles the code, run unit tests, produces artifacts that are ready to deploy...

- Eliminate the need to provision build servers
- Provides pre-packaged environments
- Allow custom environments
- Scales automatically

**Build phase transitions:**

![](https://docs.aws.amazon.com/codebuild/latest/userguide/images/build-phases.png)
```
Important

The UPLOAD_ARTIFACTS phase is always attempted, even if the BUILD phase fails.
```
## CodeDeploy
Managed deployment service that automates deploys to:
- EC2 -> Selected by tag
- On-prem servers
- Lambda functions

Also make easier:
- New Features launch
- Update lambda functions
- Avoid downtime during deployments
- Handle full process without human intervention

## Codepipeline
