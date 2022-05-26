# API Gateway

API service managed by AWS.

It allows to create an API Rest or WebSocket or import from Swagger or OPEN API 3.

You can create private APIs, Regionals or Edge Optimized.

## Integration with Lambda

You can integrate with lambda with 2 methods: Lambda or Lambda Proxy.

Lambda integration allows you to make a more deep integration, with custom payloads or explicit versions.

Lambda proxy integrations allows you to try Canary deployments.

## Stages and Deployments

Making changes in the API Gateway does not mean they're effective.
You need to make a "deployment" for them to be in effect.

Changes are deployed to "Stages" (as many as you want). Each stage has its own configuration parameters.

Example: You have 2 stages.
v1 stage points to v1 lambda version
v2 stage points to v2 lambda version

This allows to create api new versions.

Also we can use Stage Variables, that are environment variables for API Gateway.

They can be used in Lambda ARN, HTTP Endpoint or parameter mapping templates.

## Stages and Canary deployments

One of the most use cases in API Gateway is a canary deployment between stages.

Using Stage Variables to point to lambda ALias, you can map API Stages with Lambda Alias, allowing that the PROD stage points to PROD Lambda alias, that has a canary between 2 lambda versions as example.

Also you can promote a stage deployment with API Canary making a deployment to a Stage with Canary enabled.

## Throttling

By default, API Gateway has throttling by 10000 request per second, but you can limit it by Usage Plans.

## Fronting Step-Functions

API Gateway can be used to launch the Step Functions state machines.

---------------
[Go Home](../README.md)