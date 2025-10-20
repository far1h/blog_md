> Clock policy, Page replacement algorithm

![[Pasted image 20250104110430.png]]

- virtual memory (due to many processes) can exceed the capacity of the physical memory
- use backing store as a mechanism to accomodate the limited memory resources
- backing store is usually taken from the hard disk and used for memory swapping

![[Screenshot 2025-01-04 at 11.05.04 AM.png]]

- when the requested page is not in the main memory it is considered a page fault

![[Screenshot 2025-01-04 at 11.05.59 AM.png]]

- there is a need for replacement when the main memory is full and does not have the requested page

> the goal is to make the least number of replacements

how page replacement works

![[Pasted image 20250104110710.png]]

# Page Replacement Algroithms

## First-In-First-Out (FIFO) Algorithm

> provided with a collection of pages that is needed by a process, and page frames that will store the pages 

- if empty just insert the page
- if full, we replace the oldest one or the first one that went in the page frames

![[Pasted image 20250104112708.png]]

## Optimal Algorithm

> in FIFO we compared it to the previous page frame, here we try to predict the future despite receiving the page requests one by one

- replace the page frame that is used later than the others
- ex: replace 7 since 7 is used the later after 0 and 1

![[Pasted image 20250104113614.png]]
> 9 page faults

## Least Recently Used (LRU) Algorithm

> similar to FIFO by comparing to the previous page frame

- replace the page that is not used the longest or least recently used 

![[Pasted image 20250104123626.png]]

## Clock????
https://www.youtube.com/watch?v=gjLywr7GbLU&ab_channel=CS186Berkeley

![[Pasted image 20250104144351.png]]

https://youtu.be/E7pmf5pySTM?list=PLBXapj649rh9UKCBfJEyEUN5Ulvfq1s96&t=5993

Practice:
- https://rms46.vlsm.org/2/200.pdf

Answer:
- 2018-2
	- Calculate the number of faults

# Clock Policy



Hardware Control Structure 
- ﻿﻿Execution of Process 
- ﻿﻿Real and Virtual Memory 
- ﻿﻿O/S Policies for Virtual Memory 
- ﻿﻿Replacement Policy 

![[Screenshot 2024-11-15 at 8.08.31 PM.png]]
![[Screenshot 2024-11-15 at 8.09.00 PM.png]]
![[Screenshot 2024-11-15 at 8.10.08 PM.png]]
![[Screenshot 2024-11-15 at 8.11.46 PM.png]]
![[Screenshot 2024-11-15 at 8.12.49 PM.png]]![[Screenshot 2024-11-15 at 8.19.46 PM.png]]

https://youtu.be/yMRBWHWD39w?list=PLB2GiO0mMjw9J_OwnDMAqtsANzWsIylQz&t=4109

- [x] UI
- [ ] book
- [x] responsi
- [x] zulfani
- [ ] exercises
	- [ ] UI
	- [ ] assignment
	- [ ] responsi