- How do you accelerate math intensive and graphics-intensive workloads for AI/ML etc?
- Add a **[[GPU]]** to your virtual machine:  
	- High performance for <u>math intensive</u> and <u>graphics-intensive</u> workloads
	- Higher Cost  
	- (REMEMBER) Use **images with GPU libraries** (Deep Learning) installed
		- OTHERWISE, GPU will not be used
	- **GPU restrictions**:  
		- **NOT supported on all machine types** (For example, not supported on [[shared-core]] or [[memory-optimized]] machine types)
		- **On host maintenance** can only have the value "Terminate VM instance"
			- Cannot do live migration
	- Recommended **Availability policy** for GPUs 
		- Automatic restart - on

Status: #idea  
Tags:  [[gcp]], [[google-cloud-engineer]], [[Cloud]], [[cloud-compute]], [[Google Compute Engine]], [[Steps when creating a VM Instance in Google Compute Engine]]

---
# References