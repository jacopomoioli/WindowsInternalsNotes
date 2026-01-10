# Virtual Memory
Windows virtual memory provides a logical view of memory that can be different than the physical layout.
At run time, the memory manager maps virtual addresses into physical addresses.

The memory manager can page some of the memory content that is not currently used on the disk. When a thread accesses a paged virtual address, the memory manager loads the content back into the memory. This process is hidden from applications by the memory manager.