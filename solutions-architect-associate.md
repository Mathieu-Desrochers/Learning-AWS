## EC2 - Elastic Cloud Compute
Spot request with max price, Number of instances  
Launch template (AMI, instance type, key pair, network, storage)  
Type (one-time, persistent), Valid from / to dates  
Spot fleet with target capacity (number of instances, vCPUs, RAM)  
Instance type requirements (specific types, min / max vCPUs, RAM)  
Allocation strategy (lowest price, diversified, capacity optimized)  
Spot or on-demand instances  

## Solutions Architect Associate Level
Elastic IP, Fixed public IP, Max 5 per account  
Placement groups for EC2s, Cluster (all same rack)  
Spread (one per rack, max 7 per AZ), Partition (many per rack, 100s of EC2)  
ENI - Elastic Network Interface, Virtual network card, Can assign public and private IP  
Has security group, Can be attached to EC2 (eth0, eth1), Bound to AZ  
EC2 Hibernate, RAM preserved on root disk when stopped (EBS, encrypted)  

## EC2 Instance Storage
Standard HDD, st1 (throughput), sc1 (cold), Cannot be boot volumes  
General Purpose SSD, gp2 (IOPS linked to size, burst 3k, max 16k)  
gp3 (can set IOPS and throughput indenpendently, max 16k / 1 GB/s)  
Provisioned IOPS, io1 / io2 (sustained IOPS, max 32k or 64k for nitro EC2)  
io2 Block Express (sub milliseconds, 256k IOPS)  
EBS Multi-Attach, io1 / io2 only, Max 16 EC2s, Same AZ  
EBS Encryption, At rest on disk, In flight to EC2, In snapshots  
Uses KMS and AES-256, Can encrypt unencrypted volume through snapshot  
EFS, Performance mode, General purpose (low latency), Max I/O (high throughput)  
Throughput mode, Bursting (MB/s linked to size, burst 100), Provisioned  
Availability, Standard (multi AZ), One Zone, EFS One-Zone IA (-90%)  
Mount target per AZ, With security group, efs-utils in EC2 (/mnt/efs/fs1)  

## High Availability and Scalability: ELB & ASG
ALB - Application Load Balancer with hostname (xxx.region.elb.amazonaws.com)  
Scheme (internet-facing, internal), Redirections (such as HTTP to HTTPS)  
Target groups (EC2s, ECS tasks, Lambdas, Private IPs)  
With health checks (targets must return 200 OK on /health)  
Listeners with protocol and port, Rules to select target group  
Based on hostname, URL path, query string, headers  
Chain ALB security group to target inbound rules  
X-Forwarded-For / Port / Proto headers  
NLB - Network Load Balancer with static IP (one per AZ)  
Target groups (EC2s, Private IPs), Health checks (TPC, HTTP, HTTPS)  
No security group, Targets allow client CIDR with IP preservation  
Allow VPC CIDR without IP preservation and for health checks  
Gateway Load Balancer, GENEVE protocol port 6021  
Sticky Sessions (ALB), Through cookie  
Load balancer generated (configure duration, named AWSALB)  
Application-based (configure duration + name, generated by target)  
Cross-Zone Load Balancing, Traffic is spread evenly across all targets  
Without traffic is spread across AZ, then across targets in AZ  
Enabled by default for ALB with no cross AZ network charges  
SSL / TLS certificates, Supports multiple certificates (ALB, NLB)  
Uses Server Name Identification (SNI, hostname in SSL handshake)  
Deregistration delay (Connection draining), Default 300 secs  
Time to complete in flight requests before target is removed  
ASG - Auto Scaling Group, Uses CloudWatch alarms with actions  
Based on metrics (CPU, RequestCountPerTarget, Network in / out)  
Cooldown period after scaling to stabilize metrics, Default 300 secs  

## RDS + Aurora + ElastiCache
RDS Storage Auto Scaling - Less 10% free, For 5 minutes  
6 hours since last scaling, With maximum storage threshold  
RDS Read replicas - Async, Can be promoted to own DB, Application must know replicas  
RDS Multi AZ - Sync, DNS name with automatic failover, Application must retry connecting  
Cross AZ replication traffic free, Single to Multi AZ with no downtime  
Database with Authentication (password, IAM, Kerberos)  
Export logs to CloudWatch (audit, error, general, slow query)  
Maintenance window, Delete protection  
RDS Custom - Access to underlying EC2 instance (SQL Server, Oracle)  
Aurora - 
