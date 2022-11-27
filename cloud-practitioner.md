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
Effect, Action, Resource, Principal  
Create user in admin group with AdministratorAccess policy  
Account ID, Account Alias, Sign-in URL per account  
Inline policy to user directly  
Password policy, Length, Characters, Can change or not, No reuse  
MFA, Virtual device, Universal 2nd Factor, Hardware Key Fob  
Access keys for CLI and SDK, Access Key ID + Secret Access Key  
aws configure to use them  
Cloud Shell, File persistance, Upload and download  
Policies assigned to roles assigned to services (EC2, Lambda...)  
IAM Credentials Report (per account)  
IAM Access Advisor (per user), Services and last use  

## EC2 - Elastic Cloud Compute
Better safe, Billing Dashboard, Create budget with email alert  
CPU, Memory, Storage (network / hardware), Network  
AMI, Linux, Windows, Mac OS  
EC2 User Data, Bootstrap script as root on first boot  
Key Pair for SSH access  
Root volume has Delete on termination Yes  
Private IP address, Can have public that changes on stop / start  
Instance state stopped no billing, terminate to delete  
Instance types, class generation . size, m5.2xlarge  
General Purpose (t), Compute Optimized (C), Memory Optimized (R), Storage Optimized  
Security groups, Firewall with allow rules only, Inbound and outbound  
Protocol, IP Range, Port Range  
Multiple EC2 instances to multiple security groups  
Have one for SSH assigned to all EC2  
Security groups can allow other security groups, instead of IP  
21 FTP, 22 SSH SFTP, 80 HTTP, 443 HTTPS, 3389 RDP  
On demand, Pay per second, Short workload  
Reserved instances 72%, 1 or 3 years, Commit to attributes (type, region, tenancy, os)  
Convertible allows attributes change  
Saving plans 72%, 1 or 3 years, Commit to amount per hour, Above is on demand  
Spot instances 90%, lose if max price below spot  
Dedicated Host, Access to physical server, Compliance or server bound licences, Most expensive  
Dedicated Instances, Instances on hardware not shared with other accounts  
