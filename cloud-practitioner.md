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
CPU, Memory, Storage (network / hardware), Network  
AMI, Linux, Windows, Mac OS  
EC2 User Data, Bootstrap script as root on first boot  
Key Pair for SSH access  
Private IP address, Can have public that changes on stop / start  
Instance state stopped no billing, terminate to delete  
Instance types, class generation . size, Popular t2.micro  
General Purpose (t), Compute Optimized (C), Memory Optimized (R), Storage Optimized  
Security groups, Firewall with allow rules only, Inbound and outbound  
Protocol, IP Range, Port Range  
Multiple EC2 instances to multiple security groups  
Have one for SSH assigned to all EC2  
Security groups can allow other security groups, instead of IP  
21 FTP, 22 SSH SFTP, 80 HTTP, 443 HTTPS, 3389 RDP  
On demand, Pay per second, Short workload  
Reserved instances 72%, 1 or 3 years, Commit to instance attributes (type, region, tenancy, os)  
Convertible allows attributes change  
Saving plans 72%, 1 or 3 years, Commit to amount per hour, Above is on demand  
Spot instances 90%, lose if max price below spot  
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
Distribution to regions  
Uses Build and Test EC2 instances, Creates AMI image  

## Scability, Elasticity and High Availability
Scability can handle bigger loads  
Horizontal (in out) more instances, Vertical (up down) bigger instances  
Elasticity automatic scaling, High availability instances in multiple AZ  
ELB - Elastic Load Balancer  
Single point of access, Spreads load across downstream instances (target group)  
Has security group, Health checks and instance failure handling, Internet or internal  
Application (Layer 7 HTTP/S gRPC), Static URL, HTTP routing, SSL termination  
Network (Layer 4 TCP UDP), Static IP, High performance  
Gateway (Layer 3 GENEVE), Filter traffic through 3rd party security applicances  
