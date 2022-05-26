# AWS Kinesis
Is a managed alternative to Apache Kafka
Great for application logs, metrics, IoT, Clickstreams.
Great for streaming processing framework, real-time big data.
Data is automatically replicated to 3 AZ.

There are 3 services in Kinesis:
- Kinesis Stream: Low latency streaming ingest at scale
- Kinesis Analytics: Perform real-time analytics on streams using SQL
- Kinesis Firehose: Load streams into S3, Redshift, Elasticsearch...

## Data Streams
Streams are divided in Shards.

Data retention is 1 day by default, can go up to 7 days.
Multiple apps can consume the same stream.

Billing is per shard. You can have as many shards as you want.

Records are ordered per shard.
A Record is composed by DataBlob, Record Key and an unique sequence. Same record key = same shard.

Kinesis producers:
- Kinesis SDK
- Kinesis producer Library
- Kinesis Agent
- Cloudwatch Logs
- Third party producers (Spark...)

 Kinesis Consumers:
 - Kinesis SDK
 - Kinesis Library
 - Kinesis Firehose
 - Lambda
 - Third party consumers

 *KCL:*

 Kinesis Consumer Libraries uses DynamoDB to checkpoint offsets and track other workers and share the work amongst shards.
 Great for reading in a distributed manner.

 ## Kinesis Firehose

 - Fully managed service, no administration.
 - Near real time, 60 seconds latency for non full batches.
- Load data into Redshift, S3, Elastic, Splunk...
- Automatic Scaling
- Data transformation through AWS Lambda
- Supports compression when target is S3
- Pay for the data

### Data Streams vs Firehose

- Streams
  - Going to write custom code
  - Real time
  - Must manage scaling (Shard splitting/merging)
  - Data storage for 1 to 7 days
  - Use with Lambda to insert data in real-time to Elastic

- Firehose
  - Fully managed
  - Serverless data transformations
  - Near real time
  - Automated Scaling
  - No data storage


## Kinesis Data Analytics
- Autoscaling
- Managed
- Continuous: Real time
- Pay for consumption rate
- Can create streams out of the real-time queries

---------------
[Go Home](../README.md)