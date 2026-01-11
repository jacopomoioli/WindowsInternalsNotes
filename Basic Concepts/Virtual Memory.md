# Virtual Memory
Windows virtual memory provides a logical view of memory that can be different than the physical layout.
At run time, the memory manager maps virtual addresses into physical addresses.

The memory manager can page some of the memory content that is not currently used on the disk. When a thread accesses a paged virtual address, the memory manager loads the content back into the memory. This process is hidden from applications by the memory manager.

## Windows 32 bit
Total VA space: max 4gb

Default windows virtual address space allocation:
- lower half to user processes (0x00000000 thru 0x7FFFFFFF)
- upper half to windows OS (0x80000000 to 0xFFFFFFFF)
This allocation is editable using the `increaseuserva` qualifier in the boot config database (max 3gb to processes).

If more than 3gb are needed , AWE (Address Windowing Extensions)
### AWE (Address Windowing Extensions)
mechanism that allows a 32 bit application to allocate max 64gb of physical memory, mapped into the 2GB virtual space using "views" or "windows".
The management of the mapping is delegated to the application developer.

## Windows 64 bit
Total VA space: max 128TB

![[Pasted image 20260111201300.png]]
Credits to pavel yosifovich, https://www.youtube.com/watch?v=Sy9CTb7JX7k

