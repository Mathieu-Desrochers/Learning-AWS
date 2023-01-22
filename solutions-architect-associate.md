## EC2 - Elastic Cloud Compute
Spot request with max price, Number of instances  
Launch template, Type (one-time, persistent), Valid from / to dates  
Spot fleet with target capacity (number of instances, vCPUs, RAM)  
Instance requirements (specific types, min / max vCPUs, RAM)  
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
General Purpose SSD, gp2 (size and IOPS linked, burst 3k, max 16k)  
gp3 (can increase IOPS and throughput indenpendently, max 16k / 1 GB/s)  
Provisioned IOPS, io1 / io2 (sustained IOPS, max 32k or 64k for nitro EC2)  
io2 Block Express (sub milliseconds, 256k IOPS)  
EBS Multi-Attach, io1 / io2 only, Max 16 EC2s, Same AZ  
EBS Encryption, At rest on disk, In flight to EC2, In snapshots  
Uses KMS and AES-256, Can encrypt unencrypted volume through snapshot  
