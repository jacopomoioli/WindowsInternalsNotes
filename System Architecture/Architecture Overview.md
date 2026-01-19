![[Pasted image 20260117204031.png]]

User mode, Kernel Mode and Hypervisor Context are separated. Kernel and Hypervisor are both in CPU Ring 0, but the hypervisor uses VT-x, so it's isolated.

## User Mode Processes
4 types of user mode processes:
- User Processes
	- Windows 32/64 bit
	- Windows 3.1 16bit (only on 32bit)
	- MS-DOS 16bit (only on 32bit)
	- Posix 32/64 bit (deprecated)
- Service Processes
	- processes hosting win services (task scheduler, print spooler, etc)
	- independent from user logins
	- handled by the Service Control Manager
- System Processes
	- non-windows services
	- core, fixed process like logon process and session manager
- environment subsystem server process
	- various legacy subsystems, now deprecated, such as
		- OS/2
		- POSIX 
		- SUA (Subsystem for UNIX-based applications)

User mode processes (generally) do not use direct syscalls, but subsystem DLLs that acts like an interface, hiding internal native syscalls of ntdll.dll

## Kernel-Mode components
- Executive
	- base OS services: memory management, process, thread management, security, I/O, networking, IPC, etc
- Windows Kernel
	- Low level OS functions like thread scheduling, intterrupt, exception dispatching, multiprocessor synchronization
	- Provides routines and basic objects that executive uses to implement higher-level features
- Device Drivers 
	- Hardware device drivers: translate I/O function into specific hardware I/O requests
	- Non-hardware device drivers: file system, network drivers
- HAL (HW Abstraction Layer)
	- Abstraction layer that makes executive, kernel and device drivers portable between platform-specific hw differences
- USER and GDI system
	- Windows GUI
- Hypervisor

## Core Windows System Files
- Ntoskrnl.exe: executive and kernel
- Hal.dll: HAL
- win32k.sys: kernel-mode component of GUI
- Hvix64.exe, Hvax64.exe: Hypervisor
- Ntdll.dll: internal syscalls
- Kernel32.dll, Advapi32.dll, user32.dll, gdi32.dll: core win subsystem dll
- \SystemRoot\System32\Drivers\*.sys: Core driver files

## Portability
Windows portability across different hw architectures
- using a layered design: 
	- Ntoskrnl.exe contains architecture-independent functions
	- hal.dll contains architecture-dependent functions
- Using C language (+ some C++ and some assembly)

