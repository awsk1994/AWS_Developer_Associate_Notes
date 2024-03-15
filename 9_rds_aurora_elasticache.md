# RDS

* Stands for **Relational Database Service**
* a managed DB service for DB use SQL as a query language
* allows you to create databases in the cloud that are managed by AWS
    * Postgres
    * MySQL
    * MariaDB
    * Oracle
    * Microsoft SQL Server
    * IBM DB2
    * Aurora (AWS Proprietary Database)

## Advantage over using RDS versus deploying DB on EC2

* RDS is a managed service
    * automated provisioning, OS patching
    * Continuous backups and restore to specific time stamp (point in time restore)
    * Monitoring dashboards
    * read replicas for improved read performance
    * multi AZ setup for DR (disaster recovery) 
    * maintenance window for upgrades
    * scaling capacity (vertical and horizontal)
    * storage backed by EBS (gp2 or io1)
* BUT you can't SSH into your (EC2) instances

## Storage Auto Scaling

* Helps you increase storage on your RDS DB instance dynamically
* When RDS detects you are running out of free database storage, it scales automatically
* Avoid manually scaling your database storage
* You have to set **Maximum Storage Threshold** (maximum limit for DB storage)
* Automatically modify storage if:
    * Free storage is less than 10% of allocated storage
    * Low-storage lasts at least 5 minutes
    * 6 hours have passed since last modification
* Useful for applications with unpredictable workloads
* Supports all RDS database engines

## Read Replicas vs Multi AZ

### Read Replicas for read scalability

<img src="./img/9_rds_aurora_elasticache/1.png"/>

* Up to 15 read replicas
* within AZ, Cross AZ or Cross Region
* Replication is ASYNC, so reads are eventually consistent
* replicas can be promoted to their own DB
* applications must update the connection string to leverage read replicas

### Use Cases
* You have a product database that is taking on normal load
* You want to run a reporting application to run some analytics; but that would affect/slow down your production application
* Therefore, you create a read replica to run the new workload there.
* The production application is unaffected
* Read replicas are used for **SELECT** only kind of statements (not INSERT, DELETE, UPDATE)

<img src="./img/9_rds_aurora_elasticache/2.png"/>

#### Network Cost
* In AWS, there's a network cost when data goes from AZ to another (usually; but managed services sometimes don't follow this rule, and RDS is managed service)
* For RDS Read Replicas within the **same region**, you don't pay that fee

<img src="./img/9_rds_aurora_elasticache/3.png"/>

### Multi AZ (Disaster Recovery)
* SYNC replication (when write to masterA, it'll be synchronized to masterB)
* One DNS name - automatic app failover to standby 
* increase availability
* Failover in case of loss of AZ, loss of network, instance or storage failure
* No manual intervention in apps (if apps cannot connect, it'll auto-failover)
* not used for scaling (just for disaster recovery)
* **Note** The read replicas can be setup as multi-az for disaster recovery (DR)

<img src="./img/9_rds_aurora_elasticache/4.png"/>

### From Single-AZ to Multi-AZ

* Zero downtime operation (no need to stop the DB)
* Just click on "modify" for the database
* The following happens internally:
    * A snapshot is taken
    * A new DB is restored from the snapshot in a new AZ
    * Synchronization is established between the two databases

<img src="./img/9_rds_aurora_elasticache/5.png"/>
