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
- [[Pros and cons of each allocation method]]
- Use cases of each allocation method?
- [[Linked Free Space List on Disk]]

Practice:
- https://rms46.vlsm.org/2/198.pdf

Answer:
- 2019-1
	- a. 1023 + 1023 + 2 (pointer) => 3 Blocks
	- b. 1, 2, 3
	- c. 4, 5, 6, 7, 8, 9, 10, 11

Status: #idea  
Tags:  [[operating-systems#Final Exam Materials]]  

---
# References

https://youtu.be/PBkZynNIZWk?list=PLBXapj649rh9UKCBfJEyEUN5Ulvfq1s96&t=2176