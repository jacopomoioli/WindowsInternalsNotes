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

## Symmetric Multiprocessing
Windows is a Symmetric multiprocessing OS (SMP): there is no master & secondary processor and the OS itself can be scheduled to run on any processor, countrary to ASMP (Asymmetric Multi Processing) where there is one master CPU that executes the kernel and secondary processors to execute user code.

4 different types of multiprocessor systems:
- **Multicore**: Different, multiple physical cores inside the same package. 
- **Simultaneous Multi Threaded (SMT)**: support for hyperthreading (2 logical CPU on a single physical core), where each logical CPU has its own state but shared execution engine and cache.
- **Heterogeneous**: ARM-specific implementation called "big.LITTLE". differences between cores (clock speed, power draw, etc), but still able to execute same instructions. 
- **Non-Uniform Memory Access (NUMA)**: Processors grouped in nodes, each one wit its own processor and memory. Connected to the rest of the system using an interconnection bus.

## Client vs Server edtions
Windows 11
- Client Edition
    - Home
    - Pro, Pro for Education, Pro for Workstation
    - Education
    - Enterprise
    - IoT Enterprise LTSC
- Server Edition (Windows server 2025)
    - Standard
    - Datacenter
    - Azure Datacenter

Info about the running edition @ `HKLM\SYSTEM\CurrentControlSet\ProductOptions`, queryable using
- `VerifyVersionInfo` (User-mode, WinAPI, winbase.h, kernel32.dll)
- `RtlGetVersion`, `RtlVerifyVersionInfo` (Kernel-mode, WDK)

ProductType can be:
- WinNT: Windows clients
- LanmanNT: Windows server DC
- ServerNT: Windows server (No DC)

Client and server versions share core files, but different optimizations about scheduling and resource allocation at boot time and run time
