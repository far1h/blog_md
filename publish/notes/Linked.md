- There are 1-2 bytes that is used to store pointers to the next block
- Each file is a linked list of disk blocks: blocks may be scattered anywhere on the disk
- We store start and end blocks 

> good for sequential, not random

> if the block contains a pointer, usually need more than one blocks to store the file unless the size of the file < size of the block


![[Screenshot 2025-01-01 at 11.09.15 AM.png]]