# Deployment Strategies

## Single Target 

New build service substitutes old service

## All at once

Similar than Single Target, but with multi-target
Often requiring orchestration tooling.

## Minimum in service
Require Healthchecks
Deploys all instances keeping N older versions alive. 
When new instances are deployed, substitute older versions that keep alive.

## Rolling
Deploy instances in batch for N number of instances in each stage.
The deployment during all the stages needed to rolling all instances.

## Immutable
Available on Elastic Beanstalk.
Immutable deployments perform an immutable update to launch a full set of new instances running the new version of the application in a separate Auto Scaling group, alongside the instances running the old version. Immutable deployments can prevent issues caused by partially completed rolling deployments. If the new instances don't pass health checks, Elastic Beanstalk terminates them, leaving the original instances untouched.
## Blue/Green
Deploys paralelly 2 environments, blue and green, and switch between this.

Easy testing and easy rollback.

Not available in on-prem instances using CodeDeploy

## Canary
It's a blue/green progressive.
Uses Route53 weighted round robin.

---------------
[Go Home](../README.md)