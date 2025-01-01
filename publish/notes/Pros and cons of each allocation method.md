Describe the 3 file allocation method including its advantages and disadvantages

File allocation methods are crucial for managing how files are stored and accessed on secondary storage. Three common file allocation methods are contiguous allocation, chained allocation, and indexed allocation, each with distinct advantages and disadvantages. 

Contiguous allocation involves assigning a single continuous block of space for a file at the time of its creation. This method provides high performance for sequential file access, as multiple blocks can be read in a single operation. It is also efficient for direct access since the location of any block can be calculated using a simple formula. However, contiguous allocation suffers from external fragmentation, making it challenging to find sufficiently large contiguous spaces for new files. Additionally, preallocating space requires the user to predict file size, which may lead to wastage or insufficient allocation.

- fragmentation
- linear

Chained allocation, in contrast, links individual blocks of a file using pointers, with each block containing a reference to the next. This eliminates external fragmentation, as any free block can be used, and dynamic allocation makes it easy to expand files. However, sequential block access can be slow, as each block must be accessed in order to follow the chain. Direct access is particularly inefficient since reaching a specific block requires traversing the chain. Furthermore, the lack of block locality can lead to increased disk seek times, especially for systems needing to access multiple blocks consecutively. 

- no fragmentation
- slower since has to traverse to search for the block
- link can get lost and lose data

Indexed allocation combines the strengths of the other two methods by using an index block to store references to all blocks of a file. This enables both sequential and direct access, making it versatile and efficient. Additionally, indexed allocation avoids external fragmentation and supports dynamic growth of files. However, maintaining the index structure can consume significant space, especially for small files, as each file requires a dedicated index. This method may also require additional memory and processing to manage the index blocks. 

- sacrificing one block for the index, uses extra space

Overall, the choice of file allocation method depends on the specific needs of the system, such as the priority of sequential versus direct access, the frequency of file resizing, and the importance of minimizing fragmentation or space overhead.