> Partitioning, Placement Algorithm

- logical address - used by programs that are run above the OS so that they are easily accessible and standardized
- physical address - the physical RAM memory address
- logical address is translated to physical address using MMU 

## variable partition

- OS maintains information about:
	- allocated partitions (for OS and other fixed programs)
	- free partitions (hole) (for new processes)

pros and cons

fixed partitioning
- internal fragmentation
dynamic partitioning
- external fragmentation
- compact


§First-fit:  Allocate the first hole that is big enough

§Best-fit:  Allocate the smallest hole that is big enough; must search entire list, unless ordered by size 

•Produces the smallest leftover hole

§Worst-fit:  Allocate the largest hole; must also search entire list 

Produces the largest leftover hole

First-fit and best-fit better than worst-fit in terms of speed and storage utilization

pros and cons
- best fit
	- less fragmentation
	- slow to find best fit
- first fit
	- fragmentation
	- searching from the top
- next fit
	- fragmentation same as first
	- searching from the pointer

![[Pasted image 20250102164836.png]]
## Paging

similar to [[File Management]] where a disk is divided into equally sized blocks, virtual memory is divided into several pages and physical memory is divided into multiple frames with the size of pages and frames being equal or using the same size consensus

- offset: small bytes within a frame / page (1 page = 512 byte, offset-0 until offset-511)
- same between frame and page

https://rms46.vlsm.org/2/183.pdf

- [ ] UI
- [ ] book
- [ ] zulfani
- [ ] exercises
	- [ ] UI
	- [ ] assignment
	- [ ] responsi

Status: #idea  
Tags: [[operating-systems#Final Exam Materials]]

---
# References
[[🤓 William Stallings - Operating Systems#Chapter 11]]