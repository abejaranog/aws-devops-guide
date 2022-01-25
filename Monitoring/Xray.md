# AWS X-Ray

X-Ray is a tracing service that collects data about requests that your application serves, and provides tools you can use to view, filter and gain insights into data to identify issues and opportunities for optimization.

Data can be sent using the X-Ray sdk or X-Ray daemon.

A DevOps common use case of X-Ray is to using combined Cloudwatch and SNS to notify when X-Ray detects elevated levels of latency or errors in your application trace