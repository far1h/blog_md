> Partitioning, Placement Algorithm

- logical address - used by programs that are run above the OS so that they are easily accessible and standardized
- physical address - the physical RAM memory address
- logical address is translated to physical address using MMU 

## variable partition

- OS maintains information about:
	- allocated partitions (for OS and other fixed programs)
	- free partitions (hole) (for new processes)

§First-fit:  Allocate the first hole that is big enough

§Best-fit:  Allocate the smallest hole that is big enough; must search entire list, unless ordered by size 

•Produces the smallest leftover hole

§Worst-fit:  Allocate the largest hole; must also search entire list 

Produces the largest leftover hole

First-fit and best-fit better than worst-fit in terms of speed and storage utilization

## Paging

similar to [[File Management]] where a disk is divided into equally sized blocks, virtual memory is divided into several pages and physical memory is divided into multiple frames with the size of pages and frames being equal or using the same size consensus

- offset: small bytes within a frame / page (1 page = 512 byte, offset-0 until offset-511)
- same between frame and page

https://rms46.vlsm.org/2/183.pdf

 https://youtu.be/E7pmf5pySTM?list=PLBXapj649rh9UKCBfJEyEUN5Ulvfq1s96&t=5993
 
- [ ] UI
- [ ] book
- [ ] zulfani
- [ ] exercises
	- [ ] UI
	- [ ] assignment
	- [ ] responsi

- ﻿﻿Hardware Control Structure 
- ﻿﻿Execution of Process 
- ﻿﻿Real and Virtual Memory 
- ﻿﻿O/S Policies for Virtual Memory 
- ﻿﻿Replacement Policy 

![[Screenshot 2024-11-15 at 8.08.31 PM.png]]
![[Screenshot 2024-11-15 at 8.09.00 PM.png]]
![[Screenshot 2024-11-15 at 8.10.08 PM.png]]
![[Screenshot 2024-11-15 at 8.11.46 PM.png]]
![[Screenshot 2024-11-15 at 8.12.49 PM.png]]![[Screenshot 2024-11-15 at 8.19.46 PM.png]]

> Replacement Policy most likely

Status: #idea  
Tags: [[operating-systems#Final Exam Materials]]

---
# References
[[🤓 William Stallings - Operating Systems#Chapter 11]]