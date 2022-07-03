# WAF
You use AWS WAF to control how an Amazon CloudFront distribution, an Amazon API Gateway REST API, an Application Load Balancer, or an AWS AppSync GraphQL API responds to HTTP(S) web requests.

- Web ACLs – You use a web access control list (ACL) to protect a set of AWS resources. You create a web ACL and define its protection strategy by adding rules. Rules define criteria for inspecting web requests and specify how to handle requests that match the criteria. You set a default action for the web ACL that indicates whether to block or allow through those requests that pass the rules inspections.
- Rules – Each rule contains a statement that defines the inspection criteria, and an action to take if a web request meets the criteria. When a web request meets the criteria, that's a match. You can configure rules to block matching requests, allow them through, count them, or run CAPTCHA controls against them.
- Rules groups – You can use rules individually or in reusable rule groups. AWS Managed Rules and AWS Marketplace sellers provide managed rule groups for your use. You can also define your own rule groups.
After you create your web ACL, you can associate it with one or more AWS resources. The resource types that you can protect using AWS WAF web ACLs are an Amazon CloudFront distribution, an Amazon API Gateway REST API, an Application Load Balancer, and an AWS AppSync GraphQL API.

AWS WAF is available in the Regions listed at AWS service endpoints.

- For an Amazon API Gateway REST API, an Application Load Balancer, or an AWS AppSync GraphQL API, you can use any of the Regions in the list.
- For a CloudFront distribution, AWS WAF is available globally, but you must use the Region US East (N. Virginia) for all of your work. You must create your web ACL using the Region US East (N. Virginia). You must also use this Region to create any other resources that you use in your web ACL, like rule groups, IP sets, and regex pattern sets.

Some interfaces offer a region choice of "Global (CloudFront)". Choosing this is identical to choosing Region US East (N. Virginia) or "us-east-1".
You can associate a web ACL with a CloudFront distribution when you create or update the distribution itself. For information, see Using AWS WAF to Control Access to Your Content in the Amazon CloudFront Developer Guide.

You can only associate a web ACL to an Application Load Balancer within AWS Regions. For example, you cannot associate a web ACL to an Application Load Balancer that is on AWS Outposts.

---------------
[Go Home](../README.md)