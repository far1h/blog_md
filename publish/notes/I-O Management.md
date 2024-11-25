---
title: I/O Management
---
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
CSCAN
FSCAN
![[Screenshot 2024-11-15 at 7.44.30 PM.png]]![[Screenshot 2024-11-15 at 7.48.50 PM.png]]
# RAID Configuration

# Disk Arm Scheduling

# UNIX I/O

# Linux I/O

# Windows I/O


Status: #idea  
Tags: [[operating-systems#Mid Exam Materials]]

---
# References
[[🤓 William Stallings - Operating Systems#Chapter 11]]

