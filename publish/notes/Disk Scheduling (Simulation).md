- The arrangement of how we access desired cylinders
- Start from the head pointer

FIFO / FCFS
- Using the queue order

![[Pasted image 20250102125825.png]]
> (98-53)+(183-98)+(183-37)+(122-37)+(122-14)+(124-14)+(124-65)+(67-65) = total head movement of 640 cylinders

SSTF (Shorter Seek Time First)
- Find the closest

![[Pasted image 20250102131516.png]]
> (65-53)+(67-65)+(67-37)+(37-14)+(98-14)+(122-98)+(124-122)+(183-124) = total head movement of 236 cylinders


SCAN
- like an elevator scans to one end **until the edge** and scans to the other end again in reverse 
- 2 directions

![[Pasted image 20250102133132.png]]
> (53-37)+(37-14)+(65-14)+(67-65)+(98-67)+(122-98)+(124-122)+(183-124) = total head movement of 208 cylinders (not counting the head movement to 0?)


CSCAN
- scans until the edge and goes back to the start in case any were missed like a type writer
- 1 direction

FSCAN


![[Screenshot 2024-11-15 at 7.44.30 PM.png]]![[Screenshot 2024-11-15 at 7.48.50 PM.png]]

Extra info:
- Transfer rate
	- Rate at which data flow between drive and computer

- Positioning time (random-access time) consists of
	- Seek time
		- Time to find the desired cylinder/track
	- Rotational Delay
		- Time to find the desired sector

![[os-disk-performance-params.png]]
![[Screenshot 2024-11-15 at 6.54.40 PM.png]]![[Screenshot 2024-11-15 at 6.56.56 PM.png]]![[Screenshot 2024-11-15 at 6.57.59 PM.png]]![[Screenshot 2024-11-15 at 6.54.40 PM.png]]

Practice:
- Suppose there is a disk with 100 cylinders numbered 0 to 99. The current position of the head is at 15 and is moving upwards. The following I/O request arrived: 5, 0, 25, 15, 2, 85, 12 and 60. Calculate the number of disk arm / head movements that are required if the disk arm scheduling algorithm used is:
	i. SSTF (Shortest Seek Time first)
	ii. FIFO
	iii. Scan

Answer:
- ![[Screenshot 2025-01-02 at 12.44.58 PM.png]]
- ![[Pasted image 20250102124408.png]]
- ![[Screenshot 2025-01-02 at 12.44.20 PM.png]]

https://youtu.be/8Q95UCTVIVY?list=PLBXapj649rh9UKCBfJEyEUN5Ulvfq1s96&t=1375

- [x] UI
- [ ] book
- [ ] zulfani
- [ ] exercises
	- [ ] UI
	- [ ] assignment
	- [ ] responsi