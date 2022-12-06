## Cloud computing
Compute, Memory, Storage, Database, Network  
On demand, Pay-as-you-go  
Private, Public, Hybrid  
Network access, Multi-Tenancy, Elasticity, Measured  
OPEX, Economies of scale, Capacity, Agility, No data centers, Global  
IaaS, PaaS, Saas / Virtualization | OS, Runtime | Data  
Pay compute time, data stored, network out  
Regions, Availability Zones, Data centers, Edge locations (2-6 DC per AZ)  
Chose for Compliance, Proximity, Available services, Pricing  
Shared Responsability Principle, Acceptable Use Policy  

## IAM - Identity and Access Management
Root account by default, don't use  
Users in groups, no group nesting  
Policies assigned to groups or users  
Effect (Allow), Action (s3:GetObject), Resource (arn:aws:s3:...), Principal (arn:aws:iam:...)  
Create user in admin group with AdministratorAccess policy  
Account ID, Account Alias, Sign-in URL per account  
Inline policy to user directly  
Password policy, Length, Characters, Can change or not, No reuse  
MFA, Virtual device, Universal 2nd Factor, Hardware Key Fob  
Access keys for CLI and SDK, Access Key ID + Secret Access Key  
Run aws configure to use them  
Cloud Shell, File persistance, Upload and download  
Policies assigned to roles assigned to services (EC2, Lambda...)  
IAM Credentials Report (per account)  
IAM Access Advisor (per user), Services and last use  

## EC2 - Elastic Cloud Compute
Be safe, Billing Dashboard, Create budget with email alert  
CPU, Memory, Storage (network / hardware), Network, OS (Linux, Windows, Mac)  
EC2 User Data, Bootstrap script as root on first boot  
Key Pair for SSH access  
Private IP address, Can have public IP that changes on stop / start  
Instance state stopped no billing, terminate to delete  
Instance types: ClassGeneration.Size, Popular t2.micro  
General Purpose (t), Compute Optimized (C), Memory Optimized (R), Storage Optimized  
Security groups, Firewall with allow rules only, Inbound and outbound  
Protocol, IP Range, Port Range  
Multiple EC2 instances to multiple security groups  
Security groups can allow other security groups, instead of IP  
21 FTP, 22 SSH SFTP, 80 HTTP, 443 HTTPS, 3389 RDP  
On demand, Pay per second, Short workload  
Reserved instances -72%, 1 or 3 years, Commit to instance attributes (type, region, tenancy, os)  
Convertible allows attributes change  
Saving plans -72%, 1 or 3 years, Commit to amount per hour, Above is on demand  
Spot instances -90%, lost if max price below spot  
Dedicated Host, Access to physical server, Compliance or server bound licences, Most expensive  
Dedicated Instances, Instances on hardware not shared with other accounts  
Capacity Reservation, Guaranteed availability in AZ for duration, Pay use or not  

## EC2 - Instance Storage
EBS - Elastic Block Storage Volumes  
Network drive, Can attach to one EC2 instance, Locked to AZ  
Capacity in GBs and IOPS, Can be changed, Popular General Purpose SSD (gp2)  
Delete on Termination attribute (default true for root drives)  
EBS Snapshots - EBS Volume backup at point in time  
Create volume from snapshot, Can copy across AZ and regions  
Archive storage tier (-75%, 24-72h), Recycle bin (1 day to one year)  
EC2 Instance Store  
Physical drive, High Performance, Ephemeral (lost when instance stopped)  
EFS - Elastic File System  
Managed network file system, Can attach to 100s of EC2 instances, Multi AZ  
Linux only, Pay per use (no capacity planning)  
EFS IA - Infrequent Access (-92%), Lifecycle policy (60 days)  
Amazon FSx - Fully managed 3rd party file systems  
For Windows Server, SMB protocol, NTFS, AD integration  
For Lustre, Linux cluster, High performance computing (HPC)  
Both accessed from AWS or on premise  

## AMI - Amazon Machine Image
Base image for EC2 instances, Locked to one region  
Public, My AMIs, AWS Marketplace, Popular Amazon Linux 2  
Launch EC2 instance, Install software and configure, Stop instance, Build AMI  
Stored as snapshot, Deregister AMI to delete  
EC2 Instance Builder  
Pipeline with schedule (time or new package version)  
Recipe with source AMI, Components, Test components  
Insfrastructure with IAM role and instance type for pipeline run  
Distribution to multiple regions  
Uses B=build and test EC2 instances, Creates AMI image  

## Scability, Elasticity and High Availability
Scability can handle bigger loads  
Horizontal (in out) more instances, Vertical (up down) bigger instances  
Elasticity automatic scaling, High availability instances in multiple AZ  
ELB - Elastic Load Balancer  
Single point of access, Spread load across downstream instances  
Has security group, Target group (EC2 instances), Health checks to ignore failed instances  
Application (Layer 7 HTTP/S gRPC), Static URL, HTTP routing, SSL termination  
Network (Layer 4 TCP UDP), Static IP, High performance  
Gateway (Layer 3 GENEVE), Filter traffic through 3rd party security applicances  
ASG - Automatic Scaling Groups  
Automatic horizontal scaling based on minimum, desired and maximum capacity  
Registers instances to ELB, Replaces unhealthy instances  
Has launch template (EC2 instances configuration), Scaling policy  
Dynamic: Simple / Step (when CPU > 70% add 2), Target tracking (keep average CPU at 40%), Scheduled  
Predictive (machine learning to detect pattern, provision in advance)  

## S3 - Object Storage
Backups, Static website, Software delivery, Media hosting, Data lakes  
Bucket, Globally unique name, Scoped to region  
Object, Key (my-object.txt), Can simulate folders with prefix (my-folder/my-object.txt)   
Value (max 5TB, multi-part upload 5GB), Metadata (key/value pairs), VersionID  
URL (https://my-bucket.s3.ca-central-1.amazonaws.com/my-object.txt), Can be presigned  
Security with IAM policies, IAM roles, Bucket policies  
Allow, s3:GetObject, arn:aws:s3:::my-bucket/\*, Principal (* for public access)  
Bucket policies can allow cross account access, ACL at bucket or object level  
Block all public access, Safety at bucket or account level, Overrules everything  
Static website hosting, Index document, Error document  
Get bucket website endpoint (http://my-bucket.s3-website.ca-central-1.amazonaws.com)  
Bucket versioning, Versions are strings (xqkPZ...4P), Latest is returned  
Overriting key creates new object with bumped version  
Deleting adds delete marker version, can delete it to undelete  
Deleting version rollbacks to previous one  
Replication, Cross-region replicaton (CRR), Same-region replication (SRR)  
Must enable versioning, Is asynchronous  
Replication rule, Source, Filter (all), Destination, IAM role creation  
Storage classes, Per object, Anything but Standard has retrieval fee, Cost more per GET/POST  
Standard Infrequent Access (IA), Instant retrieval  
One-Zone Infrequent Access (IA), Instant retrieval, Cheaper, Less availability  
Glacier Instant Retrieval, Instant retrieval  
Glacier Flexible Retrieval, Expedited (1-5m), Standard (3-5h), Bulk (5-12h)  
Glacier Deep Archive, Standard (12h), Bulk (48h)  
Intelligent Tiering, Instant retrieval, No retrieval fee, Move objects between classes automatically  
Lifecycle rule, Filter (all), Transitions (after x day goto class y)  
Encryption, None, Server-Side, Client-Side  
Storage Gateway, Extend on-premise storage to S3  

## Snow Family - Physical Devices
Large scale data transport (in and out, S3 interface)  
Edge computing (personal offline cloud, EC2 instances)  
AWS OpsHub, Desktop application for management  
Snowcone (8TB, 2 vCPUs, 4GB memory), Data Sync agent if online later  
Snowball Edge Storage Optimized (80TB, 40 vCPUs, 80GB memory)  
Snowball Edge Compute Optimized (42TB, 52 vCPUs, 208GB memory, GPU)  
Snowmobile (100PB), Actual truck  

## Databases - Structured Data
Relational, Tables, References, SQL  
NoSQL, Flexible schema, Key-Value, Document, Graph, In-Memory, Search, JSON  
Fully managed, Backups / restores (point in time), Dashboard and alerts, Maintenance windows  
RDS - Relational Database Service, Postgres, MySql, MariaDB, Oracle, SQL Server  
Aurora, AWS proprietary Postgres or MySql (3x or 5x faster), Auto-grow (10GB), Cost more (20%)  
Snapshots, Take, Restore, Copy (other region), Share (other account)  
Read replicas (up to 5, can be across regions), Failover (replication to one other AZ, passive)  
ElastiCache, Redis or Memcached, In-memory, High performance  
DynamoDB, NoSQL, High availability (3 AZ), Serverless (no EC2 instance type selection)  
Millions req/s, Low latency (single digit ms), Standard and Infrequest Access (IA) tables  
Key-Value, Tables with primary key (Partition key + Sort key), Attributes (columns, per item)  
DAX - DynamoDB Accelerator, Specific memory cache (10x faster, microseconds)  
Global tables (2-way replication, across regions)  
Redshift, Online analytical processing (OLAP), Data warehouse, Query PBs of data using SQL, Columnar  
ERM - Elastic Map Reduce, Hadoop or Spark (batch or real-time) clusters (100s EC2 instances), Data processing  
Athena, SQL against S3 objects (CSV, JSON, Parquet), Serverless, Perfect to analyse logs  
QuickSight, AI for BI dashboard generation, Integrations with RDS, Aurora, Redshift, S3  
DocumentDB, AWS proprietary MongoDB, NoSQL using JSON  
Neptune, Graph database, Store and query relations  
QLDB - Quantum Ledger Database, Immutable, Cryptographically verifiable, No decentralization, SQL  
