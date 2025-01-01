---
title: I/O Management
---
- [ ] UI
- [ ] book
- [ ] zulfani
- [ ] exercises
	- [ ] UI
	- [ ] assignment
	- [ ] responsi

- [x] UI
- [ ] Check PPT
- [ ] Read from Binus Book
- [ ] Responsi
# I/O Devices
# Design Issues
# Disk Management
## Disk Performance Parameters
https://youtu.be/yMRBWHWD39w?si=LzeUcWur7D-nzR2B&t=1585 
https://rio18.blog.binusian.org/2016/01/02/operating-system-session-15-16-file-management-17-18-inputoutput-management-19-20-memory-management/
https://rio18.blog.binusian.org/2016/01/02/operating-system-session-15-16-file-management-17-18-inputoutput-management-19-20-memory-management/



Transfer rate
- Rate at which data flow between drive and computer

Positioning time (random-access time) consists of
- Seek time
	- Time to find the desired cylinder/track
- Rotational Delay
	- Time to find the desired sector


![[os-disk-performance-params.png]]
![[Screenshot 2024-11-15 at 6.54.40 PM.png]]![[Screenshot 2024-11-15 at 6.56.56 PM.png]]![[Screenshot 2024-11-15 at 6.57.59 PM.png]]![[Screenshot 2024-11-15 at 6.54.40 PM.png]]
## Disk Scheduling
- The arrangement of how we access desired cylinders
- Start from the head pointer

FIFO
- Using the queue order

SSTF (Shorter Seek Time First)
- Find the closest

SCAN
- like an elevator scans to the bottom until the edge and scans back up again in reverse 
- 2 directions

CSCAN
- scans until the edge and goes back to the start in case any were missed like a type writer
- 1 direction

FSCAN


![[Screenshot 2024-11-15 at 7.44.30 PM.png]]![[Screenshot 2024-11-15 at 7.48.50 PM.png]]
# RAID Configuration
- redundant array of inexpensive disks
- ex: NAS

![[Screenshot 2024-11-25 at 9.20.35 PM.png]]

> popular RAID levels are 0, 1, 5, 6 

![[Screenshot 2024-11-25 at 9.23.26 PM.png]]

> Disk striping uses a group of disks as one storage unit (COMBINED)

![[Screenshot 2024-11-25 at 9.27.28 PM.png]]

> Mirroring or shadowing keeps duplicate of each disk

![[Screenshot 2024-11-25 at 9.27.49 PM.png]]

![[Screenshot 2024-11-25 at 9.31.33 PM.png]]

> Parity means like having a backup  

![[Screenshot 2024-11-25 at 9.32.32 PM.png]]

![[Screenshot 2024-11-25 at 9.34.28 PM.png]]

![[Screenshot 2024-11-25 at 9.35.29 PM.png]]

![[Screenshot 2024-11-25 at 9.36.25 PM.png]]
# Disk Arm Scheduling

# UNIX I/O

# Linux I/O

# Windows I/O


Status: #idea  
Tags: [[operating-systems#Mid Exam Materials]]

---
# References
[[🤓 William Stallings - Operating Systems#Chapter 11]]

