# AWS Opensearch (Formerly AWS ElasticSearch)

Managed version of ElasticSearch service.

Need to run on servers. Is used in Log analytics, real time application monitoring, security analysis, full text search or indexing.

ES has node-to-node encryption and encryption at rest.

Is used with the other services of ELK Stack. (Logstash and Kibana)

- ES provide search and indexing capacity. You must specify instance types, multi-AZ, etc
- Kibana provide real-time dashboards based on ES data. Alternative to Cloudwatch Dashboards.
- Logstash is a log ingestion mechanism. Alternative to Cloudwatch Logs.

## ElasticSearch patterns

- DynamoDB -> DynamoDB Stream -> Lambda -> ES -> API Search Call

- Cloudwatch Logs -> Subscription Filter -> Lambda or Firehose -> ES