## Cloud computing
Compute, Memory, Storage, Database, Network  
On demand, Pay-as-you-go, Private, Public, Hybrid  
Network access, Multi-Tenancy, Elasticity, Measured  
OPEX, Economies of scale, Capacity, Agility, No data centers, Global  
IaaS, PaaS, Saas, Virtualization | OS, Runtime | Data  
Pay compute time, data stored, network out  
Regions, Availability Zones, Data centers, Edge locations (2-6 DC per AZ)  
Choose for Compliance, Proximity, Available services, Pricing  
Shared Responsability Principle, Acceptable Use Policy  

## IAM - Identity and Access Management
Root account by default, don't use  
Create user in admin group with AdministratorAccess policy  
Users in groups, No group nesting, Policies assigned to groups or inline to users  
Effect (Allow), Action (s3:GetObject), Resource (arn:aws:s3:...), Principal (arn:aws:iam:...)  
Account ID, Account Alias, Sign-in URL per account  
Password policy, Length, Characters, Can change or not, No reuse  
MFA, Virtual device, Universal 2nd Factor, Hardware Key Fob  
Access keys for CLI and SDK, Access Key ID + Secret Access Key, Run aws configure    
Cloud Shell, File persistance, Upload and download  
Policies assigned to roles assigned to services (EC2, Lambda...)  
IAM Credentials Report (per account)  
IAM Access Advisor (per user), Services and last use  

## EC2 - Elastic Cloud Compute
Be safe, Billing Dashboard, Create budget with email alert  
CPU, Memory, Storage (network / hardware), Network, OS (Linux, Windows, Mac)  
EC2 User Data, Bootstrap script as root on first boot  
Key Pair for SSH access, Private IP address, Can have public IP that changes on stop / start  
Instance state stopped no billing, terminate to delete  
Instance types: ClassGeneration.Size, Popular t2.micro  
General Purpose (t), Compute Optimized (C), Memory Optimized (R), Storage Optimized  
Security groups, Firewall with allow rules only, Inbound and outbound  
Protocol, IP Range, Port Range, Multiple EC2 instances to multiple security groups  
Security groups can allow other security groups, instead of IP  
21 FTP, 22 SSH SFTP, 80 HTTP, 443 HTTPS, 3389 RDP  
On demand, Pay per second, Short workload  
Reserved instances -72%, 1 or 3 years, Commit to instance type, region, tenancy, os  
Spot instances -90%, Bid on unused instances, Lost if max price below spot  
Dedicated Host, Access to physical server, Compliance or server bound licences, Most expensive  
Dedicated Instances, Instances on hardware not shared with other accounts  
Capacity Reservation, Guaranteed availability in AZ for duration, Pay use or not  

## EC2 - Instance Storage
EBS - Elastic Block Storage Volumes, Network drive, Can attach to one EC2 instance  
Capacity in GBs and IOPS, Can be changed, Popular General Purpose SSD (gp2)  
Delete on Termination attribute (default true for root drives), Locked to AZ  
EBS Snapshots - EBS Volume backup at point in time  
Create volume from snapshot, Can copy across AZ and regions  
Archive storage tier (-75%, 24-72h), Recycle bin (1 day to one year)  
EC2 Instance Store, Physical drive, High Performance, Ephemeral (lost when instance stopped)  
EFS - Elastic File System, Managed network file system, Can attach to 100s of EC2 instances  
Linux only, Pay per use (no capacity planning), Multi AZ    
EFS IA - Infrequent Access (-92%), Lifecycle policy (60 days)  
Amazon FSx - Fully managed 3rd party file systems  
For Windows Server, SMB protocol, NTFS, AD integration  
For Lustre, Linux cluster, High performance computing (HPC)  
Both accessed from AWS or on-premise  

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
Uses build and test EC2 instances, Creates AMI image  

## Scability, Elasticity and High Availability
Scability can handle bigger loads  
Horizontal (in / out) more instances, Vertical (up/down) bigger instances  
Elasticity automatic scaling, High availability instances in multiple AZ  
ELB - Elastic Load Balancer, Single point of access, Spread load across downstream instances  
Has security group, Target group (EC2 instances), Health checks to ignore failed instances  
Application (Layer 7 HTTP/S gRPC), Static URL, HTTP routing, SSL termination  
Network (Layer 4 TCP UDP), Static IP, High performance  
Gateway (Layer 3 GENEVE), Filter traffic through 3rd party security applicances  
ASG - Automatic Scaling Groups, Horizontal scaling based on minimum, desired and maximum capacity  
Registers instances to ELB, Replaces unhealthy instances  
Has launch template (EC2 instances configuration), Scaling policy  
Dynamic: Simple / Step (when CPU > 70% add 2), Target tracking (keep average CPU at 40%)  
Scheduled, Predictive (machine learning to detect pattern, provision in advance)  

## S3 - Simple Storage Service
Backups, Static website, Software delivery, Media hosting, Data lakes  
Bucket, Globally unique name, Scoped to region  
Object with key (my-object.txt), Can simulate folders with prefix (my-folder/my-object.txt)   
Value (max 5TB, multi-part upload 5GB), Metadata (key / value pairs)  
URL (https://bucket.s3.ca-central-1.amazonaws.com/object.txt), Can be presigned  
Pay per number / size of objects, number of requests, data transfered out  
Security with IAM policies, IAM roles, Bucket policies (principal * for public access)  
Bucket policies can allow cross account access, ACL at bucket or object level  
Block all public access, Safety at bucket or account level, Overrules everything  
Static website hosting, Index document, Error document, s3-website.ca-central-1.amazonaws.com  
Versioning with string IDs (xqkPZ...4P), Deleting adds delete marker version  
Replication, Cross-region replicaton (CRR), Same-region replication (SRR)  
Rule with source, Filter (all), Destination, Must enable versioning, Is asynchronous  
Storage classes, Per object, Anything but Standard has retrieval fee  
Standard Infrequent Access (IA), Instant retrieval  
One-Zone Infrequent Access (IA), Instant retrieval, Cheaper, Less availability  
Glacier Instant Retrieval, Instant retrieval  
Glacier Flexible Retrieval, Expedited (1-5m), Standard (3-5h), Bulk (5-12h)  
Glacier Deep Archive, Standard (12h), Bulk (48h)  
Intelligent Tiering, Instant retrieval, No retrieval fee, Move objects between classes automatically  
Lifecycle rule with filter (all), Transitions (after x day goto class y)  
Encryption (None, Server-Side, Client-Side)  
Storage Gateway, Extend on-premise storage to S3  

## Snow Family - Physical Devices
Large scale data transport (in and out, S3 interface)  
Edge computing (personal offline cloud, EC2 instances)  
AWS OpsHub, Desktop application for management  
Snowcone (8TB, 2 vCPUs, 4GB memory), Data Sync agent if online later  
Snowball Edge Storage Optimized (80TB, 40 vCPUs, 80GB memory)  
Snowball Edge Compute Optimized (42TB, 52 vCPUs, 208GB memory, GPU)  
Snowmobile (100PB), Actual truck  

## Databases
Relational, Tables, References, OLTP, SQL  
NoSQL, Flexible schema, Key-Value, Document, Graph, In-Memory, Search, JSON  
RDS - Relational Database Service, Postgres, MySql, MariaDB, Oracle, SQL Server  
Aurora, AWS proprietary Postgres or MySql (3x or 5x faster), Auto-grow (10GB), Cost more (20%)  
Read replicas (up to 5, can be across regions), Failover (replication to one other AZ, passive)  
Pay per hour, EC2 instance type, GBs / month, On demand or reserved (1 - 3 years)  
ElastiCache, Redis or Memcached, In-memory, High performance  
DynamoDB, Key-Value, High availability (3 AZ), Serverless (no EC2 instance type selection)  
Tables with primary key (partition key + sort key), Attributes (columns, per item)  
DAX - DynamoDB Accelerator, Specific memory cache (10x faster)  
Global tables (2-way replication, across regions)  
Redshift, Online analytical processing (OLAP), Data warehouse, Query PBs of data using SQL, Columnar  
ERM - Elastic Map Reduce, Hadoop or Spark (batch or real-time) clusters (100s EC2 instances), Data processing  
Athena, SQL against S3 objects (CSV, JSON, Parquet), Serverless, Perfect to analyse logs  
QuickSight, BI dashboard generation, Supports RDS, Aurora, Redshift, S3  
DocumentDB, AWS proprietary MongoDB, NoSQL using JSON  
Neptune, Graph database, Store and query relations  
QLDB - Quantum Ledger Database, Immutable, Cryptographically verifiable, Centralized, SQL  
Managed Blockchain, Public or private network, Hyperledger Fabric, Ethereum, Decentralized    
Glue, Managed extract transform and load (ETL), Data catalogs  
DMS - Database Migration Service, Runs on EC2 instances, Homogeneous or Heterogeneous  

## Other Compute Services
ECS - Elastic Container Service, Runs docker, Must provision EC2 instances  
Starts, stops and spreads containers, Integrates with Application Load Balancer  
Fargate, Serverless, No EC2 instances to manage, Pay based on allocated vCPU / RAM  
ECR - Elastic Container Registry, Private docker images registry  
Lambda, Event driven, Pay per calls and duration (in GBs, RAM * seconds)  
Increasing RAM also increase CPU and network, All languages, Lambda Container Image  
Function with code, test events, timeout (max 15m), IAM role (for CloudWatch logs)  
API Gateway, REST or websocket, Authentication and Authorization, API Keys, Throttling, Can expose lambdas  
Batch, Automatically provision EC2 instances (can be spot), Jobs as docker images, Runs on ECS  
Lightsail, Baby alternative to EC2 / EBS/ RDS, Templates for LAMP, Node.js, WordPress  

## Managing Infrastructure at Scale
CloudFormation, Declarative, Infrastructure as code, Nice for source control  
Provisions in the right order, Easy to delete / recreate for costs saving, Diagrams  
Stack with name, Template for resources (json / yaml), Parameters (!Ref Color)  
Apply updates with changet preview, Events (create_in_progress, create_complete)  
CDK - Cloud Development Kit, Infrastructure in programming language  
If/Loop/Functions, Compiled by CDK CLI to json / yaml  
Beanstalk, Runs code on typical architectures (LB + ASG + RDS), PaaS  
Creates CloudFormation stack with EC2 instances, Health monitoring with CloudWatch  
Application with name, Platform (language / os), Code (upload), Public URL  
Can edit configuration, Upload new code version, Multiple environments (dev/prod)  

## Software Development
Code Commit, Managed git repositories  
Code Build, Compile code, Run tests, Build packages, Pay for build time  
Code Artefact, Store dependencies and built packages (nuget, npm, pip)  
Code Deploy, EC2 instances or on-premise, Upgrades versions, Requires Code Deploy Agent  
Code Pipeline, Basis for CI/CD, orcherstration for the steps above  
Code Star, All in one, Quick start with dashboard and best practices  
Provisions Beanstalk with CloudFormation stack with EC2 instances  
Cloud9, Browser IDE, Code and debug, Multi-users collaboration, Runs on EC2 instances  

## Systems Management
SSM - Systems Manager, Manage fleet of computers, EC2 instances or on-premise  
Patching, Running commands, Applying configuration, Windows and Linux  
Requires SSM Agent (installed by default on Amazon Linux)  
SSM Session Manager, Shell to computer through SSM Agent, No SSH or Bastion  
EC2 instances require IAM role with AmazonSSMManagedInstanceCore policy  
OpsWorks, Managed Chef or Puppet, 3rd party alternatives to SSM  

## Global Infrastructure
Multiple regions or points of presence (edge locations)  
Less latency, Disaster recovery, Attack protection  
Route 53, Managed DNS, Domain name registration, A (host to IPv4), AAAA (host to IPv6)  
CNAME (host to host), Alias (host to AWS resource, ELB, CloudFront, RDS)  
Hosted zone with record set, Routing policies (per record)  
Simple (no health check, all others yes), Weighted (load balancing like 70% 30%)  
Latency (we specify region of IP), Failover (primary and secondary)  
CloudFront, CDN, Caching proxy with TTL, Static content at edge locations  
Distribution with domain name (cloudfront.net), Origin domain (S3 bucket URL, custom HTTP URL)  
Origin access (public, Origin Access Control + S3 bucket policy), DDoS protection with WAF and Shield  
Pay per TBs / month, number of HTTP requests, Varies by continent  
S3 Transfer Acceleration, Download and upload to S3 bucket through edge locations  
Global Accelerator, Internet until edge location, AWS network until resource  
Provides 2 Anycast IP to send traffic to edge locations  
Outposts, Server racks managed by AWS, Run AWS services on-premise  
Local Zones, At a precise geographical location (us-east-1-bos-1, Boston)  
Wavelength Zones, At the edge of 5G networks (us-east-1-wl1-bos-wlz-1, Boston)  
Architectures, Single region single AZ (easy), Multi AZ (high availability)  
Multi regions active-passive (low read latency), Active-active (low write latency)  

## Cloud Integrations
Synchronous vs asynchronous, Scale services independently  
SQS - Standard Queue, Multiple producers and consumers (ASG based on queue length)  
Messages are received by one (must delete once processed), Retention (max 14d)  
SNS - Simple Notification Service, Multiple publishers and subscribers, No retention  
Messages are received by all, Topic with name, Subscriptions (Lambda, HTTP, Email, Mobile)  
MQ, Managed RabbitMQ or ActiveMQ (MQTT, AMQP), 3rd party alternatives to SQS and SNS  
Kinesis, Real-time streams, Data Streams to ingest (100k sources)  
Data Analytics to run SQL, Firehost to persist (S3, Redshift, Elastic Search)  

## Monitoring
CloudWatch Metrics, Produced by all AWS services, Display in dashboards    
EC2 (Status check, CPU utilization), EBS (Number of reads, writes)  
S3 (Bucket size in bytes), Billing (Estimated charges, only in us-east-1)  
CloudWatch Alarms with metric, Statistic over preriod (max, average, 5m)  
Conditions (> 95%), Actions (EC2, ASG or SNS)  
CloudWatch Logs, Real-time monitoring, Collect from Lambda  
Beanstalk, ECS, EC2 by installing CloudWatch Logs Agent (with IAM role)  
Log groups with streams with events, Retention  
EventBridge, React to events, Rule with name, Source type  
Event pattern (AWS service and event type), Schedule (cron or interval)  
Target (Lambda, SNS, SQS), From event buses (AWS, partner or custom)  
CloudTrail, Logs API calls by users (from console, SDK, CLI), Enabled by default  
Event history with events with username, time, full API request body  
CloudTrail Insight, Automated analysis, Export to CloudWatch or S3 for retention  
X-Ray, Distributed tracing, Troubleshoot performance, Understand dependencies (graph)  
CodeGuru Reviewer, AI powered code reviews (static code analysis)  
CodeGuru Profiler, CPU and memory utilization (run time analysis), Minimal overhead  
Service Health Dashboard, All services per region, Current status and history  
Personal Health Dashboard, Ones we use only, Scheduled activities, Bell icon, View all alerts  

## Networking
VPC, Private network (in region) with CIDR range (172.31.0.0/16)  
Subnets with CIDR subrange (in AZ), Public (accessible from internet) or private  
Internet Gateway, Internet access, Inside VPC, Route from public subnet  
NAT Gateway, Outbound internet access, Inside public subnet, Route from private subnet  
Route Tables, VPC or subnet, Destination (172.31.0.0/16, 0.0.0.0/0), Target (local, gateway)  
Network ACL, At subnet level, Allow and deny rules, IP only, Stateless  
Security Groups, Assigned to EC2 instances, Allow rules only, IP or security groups, Stateful  
VPC Flow Logs, Capture IP traffic information, Diagnose connectivity issues  
VPC Peering, Connect VPCs on AWS network, No CIDR overlap, Cross region or account, Nontransitive  
VPN Endpoint, AWS services are accessed through internet even from AWS resources  
Type (gateway for S3 and DynamoDB, interface for all others), Provides access through AWS network  
PrivateLink, Vendor VPC (Network load balancer), Consumer VPC (Elastic Network Interface), No peering  
Site to Site VPN, Through internet, Customer Gateway (CGW) to Virtual Private Gateway (VGW)  
Direct Connect (DX), Through private physical connection  
Client VPN, Use OpenVPN from computer to connect to VPC  
Transit Gateway, Simpler hub-and-spoke connection, Supports 1000s VPCs, VPN and DX  
Pay for traffic, Free in, Free out same AZ, Paid out other AZ (cheaper on private IP)  

## Security and Compliance
Shared Responsability Model, AWS security of the cloud, Customer security in the cloud  
Shield, Distributed Denial of Service (DDoS), Route 53, CloudFront, API Gateway, Load Balancer  
Common TCP attacks (layer 4), Standard (free, activated all accounts)  
Advanced (3k / month, sophisticated attacks, response team, spike fees not charged)  
WAF - Web Application Firewall, Common HTTP attacks (layer 7)  
Rules on IP, headers, body, URI, SQL injection, Cross-Site Scripting, geo-match, rates  
Penetration testing, Allowed on some services, But no prohibited activities (DDoS, flooding)  
KMS - Key Management Service, Customer Master Keys, Some services opt-in or required  
AWS Managed Keys, Default key per service (aws/ebs, aws/sns), Free, We don't know them  
Customer Managed Keys, With type (symmetric, asymmetric), Origin (KMS, external, CloudHSM), Rotation  
Custom Key Store, CloudHSM (Hardware Secret Module), We manage keys with CloudHSM client  
ACM - AWS Certificate Manager, SSL / TLS certificates, Public / Private, Automatic renewal  
Secrets Manager, Store secrets, Type RDS (username / password / which database)  
Type other (key / value pairs or plaintext), Automatic rotation (x days), Can retrieve by API calls  
AWS Artifact, Download compilance documents, Reports (ISO, PCI, SOC), Agreements (BAA, HIPAA)  
GuardDuty, AI analysing logs (CloudTrail, VPC Flow, DNS) to detect anomalies (also CryptoCurrency attacks)  
Inspector, Automatic security assessments using SSM, Packages CVE, Network reachability, EC2, ECR and Lambda  
AWS Config, Track configuration compliance over time, With resource type  
Rules (restricted-ssh, s3-bucket-public-read-prohibited), Report of non-compliant resources  
Macie, Scans S3 buckets for personally identifiable information (PII)  
Security Hub, Dashboard to aggregate GuardDuty, Inspector, Macie from multiple accounts  
Detective, Identifies root cause of security issues, Feeds from sources above  
AWS Abuse, Report AWS resources for spam, port scanning, DDoS, intrusion attempts, content  
Root User Provileges, Change email or password, Close account, Change support plan, Marketplace  

## Machine Learning
Rekognition, Find people, text or objects in images or videos  
Transcribe, Speech to text, Automatic language identification, Can automatically strip PII  
Polly, Text to speech, Neural (most human like) or standard, Voice selection  
Translate, Natural and accurate text translation  
Lex, Like Alexa, Speech recognition and language understanding  
Connect, Virtual contact center, Bots accepting phone calls  
Comprehend, Natural Language Processing (NLP), Finds language, key phrases, sentiment, topic  
SageMaker, Managed service to build ML models, Label data, Build model, Train, Apply  
Forecast, Input historical time-series data, Builds model, Makes prediction  
Kendra, Like google, Document search service, Indexes, Answers questions, Incremental learning  
Personalize, Like Amazon.com, Real-time personalized recommendations  
Textract, Extract text, handwriting, data from scanned documents (OCR)  

## Account Managenemt, Billing and Support
Organizations, Manage multiple accounts, Consolidated billing, Volume discounts, Reserved EC2  
Organization Units (OU), Root contains master account, Can be nested, Contains child accounts  
Service Control Policies (SCP), Applies to OU or account (but not master), Same syntax IAM policies  
SCP Hierarchy, Inheritance from OU to account, Denies cannot be allowed deeper  
Control Tower, Automatic organizations, Landing zone with master, log and audit accounts, SSO to all  
Controls (guardrails), Automatic SCP, Report of non-compliant OUs  
Pricing models, Pay as you go, Save when you reserve, Pay less by using more, Pay less as AWS grows  
EC2 Savings plans -72%, 1 or 3 years, Commit to amount per hour and family (T1, M5), Above is on demand  
Compute Savings Plan -66%, Commit to amount per hour (EC2, Fargate, Lambda), Regardless region, family or size  
Machine Learning Savings Plan, Services like SageMaker  
Pricing Calculator, Estimate solution costs, Input services and pricing strategy  
Billing Dashboard, Costs for current month by service, Free tier usage  
Cost Explorer, Costs over time by resource, Savings plan recommendation, 12 months forecast  
Cost and Usage Report, Most comprehensive information (CSV file), Services, IAM users, Hourly  
Cost Allocation Tags, Use tags for filtering and grouping in Cost Explorer  
Cost Optimizer, Recommend optimal AWS resources based on workloads (EC2, ASG, EBS, Lambda)  
