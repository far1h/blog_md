---
date: 2024-11-12
---
> File allocation algorithms (contiguous, chained, indexed)

- File system resides on secondary storage (disks)
- File system divides disks into several blocks of sectors (usually 512 bytes)
- An allocation method refers to how disk blocks are allocated for files:
	- [[Contiguous]] (where the blocks that we use to store a file is **ordered**)
	- [[Linked]] (where one block is not entirely used to store data but pointers as well)
	- [[Indexed]] (where there is one block that stores the pointers to the data blocks)

Extra info:
- [[Linked Free Space List on Disk]]

https://youtu.be/PBkZynNIZWk?list=PLBXapj649rh9UKCBfJEyEUN5Ulvfq1s96&t=2176

Status: #idea  
Tags:  [[operating-systems#Final Exam Materials]]  

---
# References