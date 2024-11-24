---
date: 2024-11-24
---
> How do you keep your VM instances running when a host system needs to be updated (a soware or a hardware update needs to be performed)?

- Your running instance is migrated to another host in the same zone 
- Does NOT change any attributes or properties of the [[Virtual Machine|VM]] 
- SUPPORTED for instances with local SSDs  
- NOT SUPPORTED for [[GPU|GPUs]] and [[Preemtible Instances|preemptible instances]]

Important Configuration - **[[Availability Policy]]**:  
- **On host maintenance**: What should happen during periodic infrastructure maintenance?
	- Migrate (default): Migrate VM instance to other hardware 
	- Terminate: Stop the VM instance
- **Automatic restart** - Restart VM instances if they are terminated due to non-user-initiated reasons (maintenance event, hardware failure etc.)

Status: #idea  
Tags:  [[gcp]], [[google-cloud-engineer]], [[cloud]], [[cloud-migration]], [[Google Compute Engine]]

---
# References