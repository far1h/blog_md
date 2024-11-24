---
date: 2024-11-24
---
How Spot Instances works in [[azure|Azure]]: 
- ﻿﻿Buy <u>unused compute capacity</u> for [[Virtual Machine|VMs]] at savings
- ﻿﻿Ideal for **interruptible workloads**
- ﻿﻿**No specific completion time** needed

How Spot Instances works in [[gcp|GCP]]: 
- **Spot [[Virtual Machine|VMs]]**: Latest version of [[Preemtible Instances|preemptible VMs]] 
- **Key Difference**: Does not have a maximum runtime  
	- Compared to traditional [[Preemtible Instances|preemptible VMs]] which have a maximum runtime of 24 hours
- Other features similar to [[Preemtible Instances|traditional preemptible VMs]] 
	- May be reclaimed at any time with 30-second notice  
	- NOT always available  
	- Dynamic Pricing: 60 - 91% discount compared to on-demand VMs
	- Free Tier credits not applicable

Status: #idea  
Tags: [[az-900]], [[azure]], [[cloud]], [[cloud-billing]], [[AWS EC2]], [[Azure Virtual Machines]], [[gcp]], [[google-cloud-engineer]],

---
# References