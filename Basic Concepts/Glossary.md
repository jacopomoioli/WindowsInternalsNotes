## Windows API Functions
documented subroutines of WinAPI
## Native System Services, Syscalls
undocumented subroutines, callable from usermode, that are internally used by [[#Windows API Functions]]
## Kernel Support Functions
Subroutines callable from kernel mode only
## Windows Services
processes started by the Windows Service Control Manager (i.e. task scheduler service)
## Dynamic Link Libraries
Callable subroutines linked together as a binary PE file, that can be loaded dynamically by processes.
Windows ensures that there is only a single in-memory copy of the DLL code, shared between multiple processes.