# Kernel vs User Mode
Windows uses 2 processor access modes:
- User Mode (x86 Ring 3)
	- where user application code runs
	- each process has its own private memory space
- Kernel Mode (x86 Ring 0)
	- where the OS code runs
	- single address space shared between OS and device drivers
		- Different components in kernel mode do not have any security boundary between each others -> **Third party kernel device drivers  have complete access** (driver signing & driver verifier have been created to mitigate this )
		- 

Only 2 modes even if the underlying architecture supports more than 2 for compatibility reasons(es. x86 supports 4, but ARM and MIPS/Alpha only 2)

Each virtual memory page is tagged 
- with the appropriate processor access mode that must be used to R/W that page
	- System space pages (kernel mode) accessible only from kernel mode
	- User space pages accessible from both user mode and kernel mode
- with the eventual no execute flag (if the cpu supports it)
	- Windows DEP (Data Execution Prevention)

User applications switch from user mode to kernel mode using system calls