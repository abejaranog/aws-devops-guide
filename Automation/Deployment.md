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

## Blue/Green
Deploys paralelly 2 environments, blue and green, and switch between this.

Easy testing and easy rollback.

Not available in on-prem instances using CodeDeploy

## Canary
It's a blue/green progressive.
Uses Route53 weighted round robin.