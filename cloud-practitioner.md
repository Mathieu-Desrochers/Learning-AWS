## What is cloud computing
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
Policies assignes to groups or users  
Effect, Action, Resource, Principal  
Create user in admin group with AdministratorAccess policy  
Account ID, Account Alias, Sign-in URL per account  
Inline policy to user directly  
Password policy, Length, Characters, Can change or not, No reuse  
MFA, Virtual device, Universal 2nd Factor, Hardware Key Fob  
Access keys for CLI and SDK, Access Key ID + Secret Access Key  
aws configure to use them  
Cloud Shell, File persistance, upload and download  
Policies assignes to roles assigned to services (EC2, Lambda...)  
IAM Credentials Report (per account)  
IAM Access Advisor (per user), Services and last use  

## EC2 - Elastic Cloud Compute
Better safe, Billing Dashboard, Create budget with email alert  
CPU, Memory, Storage (network/hardware), Network  
Linux, Windows, Mac OS (AMI)  
EC2 User Data, Bootstrap script as root on first boot  
Key Pair for SSH access  
Root volume has Delete on termination Yes  
Private IP address, Can have public that changes on stop/start  
Instance state stopped no billing, terminate to delete  
