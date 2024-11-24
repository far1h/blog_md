---
date: 2024-11-24
---
How Preemtible Instances works in [[gcp|GCP]]: 
- **Short-lived cheaper** (upto 80%) compute instances 
	- Can be stopped by GCP any time (preempted) within 24 hours
	- Maximum time for running is 24 hours
	- Instances get <u>30 second warning</u> (to save anything they want to save) 
- **Use Preempt VM's** if:
	- Your applications are **[[fault tolerant]]**  
	- You are very **cost sensitive**  
	- Your workload is **NOT immediate**  
	- Example: Non immediate batch processing jobs

**RESTRICTIONS:** 
- NOT always available
- NO SLA and CANNOT be migrated to regular [[Virtual Machine|VMs]] 
- NO Automatic Restarts  
- Free Tier credits not applicable

> Similar to AWS [[Spot Instances]]

Status: #idea  
Tags:  [[gcp]], [[google-cloud-engineer]], [[cloud]], [[cloud-billing]], [[alibaba cloud]]

---
# References
