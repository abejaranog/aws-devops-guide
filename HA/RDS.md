# RDS
Amazon Relational Database Service (Amazon RDS) is a web service that makes it easier to set up, operate, and scale a relational database in the AWS Cloud. It provides cost-efficient, resizable capacity for an industry-standard relational database and manages common database administration tasks.

## Multi-AZ deployments
Multi-AZ deployments can have one standby or two standby DB instances. When the deployment has one standby DB instance, it's called a Multi-AZ DB instance deployment. A Multi-AZ DB instance deployment has one standby DB instance that provides failover support, but doesn't serve read traffic. When the deployment has two standby DB instances, it's called a Multi-AZ DB cluster deployment. A Multi-AZ DB cluster deployment has standby DB instances that provide failover support and can also serve read traffic.

In a Multi-AZ DB instance deployment, Amazon RDS automatically provisions and maintains a synchronous standby replica in a different Availability Zone. The primary DB instance is synchronously replicated across Availability Zones to a standby replica to provide data redundancy and minimize latency spikes during system backups. 

The high availability option isn't a scaling solution for read-only scenarios. You can't use a standby replica to serve read traffic. To serve read-only traffic, use a Multi-AZ DB cluster or a read replica instead.

## Replicating backups on another AWS Region
For added disaster recovery capability, you can configure your Amazon RDS database instance to replicate snapshots and transaction logs to a destination AWS Region of your choice. When backup replication is configured for a DB instance, RDS initiates a cross-Region copy of all snapshots and transaction logs as soon as they are ready on the DB instance.

## Disaster Recovery
- RTO: Recovery time objective (RTO) represents how many hours it takes you to return to a working state after a disaster.
- RPO: Recovery point objective (RPO) which is also expressed in hours, represents how much data you could lose when a disaster happens. For example, an RPO of 1 hour means that you could lose up to 1 hour’s worth of data when a disaster occurs.

| Feature           | RTO    | RPO    | Cost   | Scope         |
|-------------------|--------|--------|--------|---------------|
| Automated Backups | Good   | Better | Low    | Single Region |
| Manual Snapshot   | Better | Good   | Medium | Cross-Region  |
| Read Replicas     | Best   | Best   | High   | Cross-Region  |


# Amazon Aurora
Amazon Aurora (Aurora) is a fully managed relational database engine that's compatible with MySQL and PostgreSQL.

An Amazon Aurora DB cluster consists of one or more DB instances and a cluster volume that manages the data for those DB instances. 

- Primary DB instance – Supports read and write operations, and performs all of the data modifications to the cluster volume. Each Aurora DB cluster has one primary DB instance.
- Aurora Replica – Connects to the same storage volume as the primary DB instance and supports only read operations. Each Aurora DB cluster can have up to 15 Aurora Replicas in addition to the primary DB instance. Maintain high availability by locating Aurora Replicas in separate Availability Zones. Aurora automatically fails over to an Aurora Replica in case the primary DB instance becomes unavailable. You can specify the failover priority for Aurora Replicas. Aurora Replicas can also offload read workloads from the primary DB instance.

## Replication
When you create a second, third, and so on DB instance in an Aurora provisioned DB cluster, Aurora automatically sets up replication from the writer DB instance to all the other DB instances. These other DB instances are read-only and are known as Aurora Replicas.

Aurora Replicas have two main purposes. You can issue queries to them to scale the read operations for your application. That way, Aurora can spread the load for read-only connections across as many Aurora Replicas as you have in the cluster. Aurora Replicas also help to increase availability. If the writer instance in a cluster becomes unavailable, Aurora automatically promotes one of the reader instances to take its place as the new writer.

If the primary instance in a DB cluster using single-master replication fails, Aurora automatically fails over to a new primary instance in one of two ways:

- By promoting an existing Aurora Replica to the new primary instance
- By creating a new primary instance

If the DB cluster doesn't contain any Aurora Replicas, then the primary instance is recreated in the same AZ during a failure event. 

## High Availability
When data is written to the primary DB instance, Aurora synchronously replicates the data across Availability Zones to six storage nodes associated with your cluster volume. 

For high availability across multiple AWS Regions, you can set up Aurora global databases. Each Aurora global database spans multiple AWS Regions, enabling low latency global reads and disaster recovery from outages across an AWS Region. Aurora automatically handles replicating all data and updates from the primary AWS Region to each of the secondary Regions.

### Global failover
An Aurora global database provides more comprehensive failover capabilities than the failover provided by a default Aurora DB cluster. By using an Aurora global database, you can plan for and recover from disaster fairly quickly. Recovery from disaster is typically measured using values for RTO and RPO.

- Recovery time objective (RTO) – The time it takes a system to return to a working state after a disaster. In other words, RTO measures downtime. For an Aurora global database, RTO can be in the order of minutes.
- Recovery point objective (RPO) – The amount of data that can be lost (measured in time). For an Aurora global database, RPO is typically measured in seconds. With an Aurora PostgreSQL–based global database, you can use the rds.global_db_rpo parameter.

With an Aurora global database, there are two different approaches to failover depending on the scenario.

- Manual unplanned failover ("detach and promote") To recover from an unplanned outage or to do disaster recovery (DR) testing, perform a cross-Region failover to one of the secondaries in your Aurora global database. The RTO for this manual process depends on how quickly you can perform the tasks listed in Recovering an Amazon Aurora global database from an unplanned outage. The RPO is typically measured in seconds, but this depends on the Aurora storage replication lag across the network at the time of the failure.
- Managed planned failover – This feature is intended for controlled environments, such as operational maintenance and other planned operational procedures. By using managed planned failover, you can relocate the primary DB cluster of your Aurora global database to one of the secondary Regions. Because this feature synchronizes secondary DB clusters with the primary before making any other changes, RPO is 0 (no data loss).

### Recovering an Aurora global database from an unplanned outage
To fail over to a secondary cluster after an unplanned outage in the primary Region

- Stop issuing DML statements and other write operations to the primary Aurora DB cluster in the AWS Region with the outage.
- Identify an Aurora DB cluster from a secondary AWS Region to use as a new primary DB cluster. If you have two or more secondary AWS Regions in your Aurora global database, choose the secondary cluster that has the least lag time.
- Detach your chosen secondary DB cluster from the Aurora global database.
- Removing a secondary DB cluster from an Aurora global database immediately stops the replication from the primary to this secondary and promotes it to a standalone provisioned Aurora DB cluster with full read/write capabilities. Doing this avoids data inconsistencies among the DB clusters in the Aurora global database (split-brain issues).
- Reconfigure your application to send all write operations to this now standalone Aurora DB cluster using its new endpoint. If you accepted the provided names when you created the Aurora global database, you can change the endpoint by removing the -ro from the cluster's endpoint string in your application.
- This Aurora DB cluster becomes the primary cluster of a new Aurora global database when you start adding Regions to it in the next step.
- Add an AWS Region to the DB cluster. When you do this, the replication process from primary to secondary begins.
- Add more AWS Regions as needed to recreate the topology needed to support your application.

---------------
[Go Home](../README.md)