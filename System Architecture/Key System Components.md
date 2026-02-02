# Key System Components

## Environment Subsystems
Each env subsystems provides a different subset of native windows services. Each executable image is bound to a single subsystem, specified with the linker's `SUBSYSTEM` option.

Usermode applications do not call native syscalls directly, but they go thru one or more subsystems DLLs, e.g. kernel32.dll, advapi32.dll, user32.dll, gdi32.dll. When a subsystem dll's function is invoked, three different options:
1) Function is entirely implemented in user-mode
2) Function requires the use of one or more native syscalls
    - e.g. `ReadFile` calls the undocumented, native, internal `NtReadFile`, `WriteFile` calls `NtWriteFile` 
3) Function requires the execution of a task in the environment subsystem process. A client/server request is sent to the environment subsystem via a ALPC message.

Sometimes, both 2 and 3.

## Windows Subsystem
Display I/O (GUI) implemented in the Windows subsystem even if conceptually every subsystem should be independent => reality is that windows subsystem is REQUIRED for every other subsystem, and therefore it's a CRITICAL PROCESS (system crashes if process exits).

Several Components:
- for each session, csrss.exe (environment subsystem process) loads four dlls:
    - basesrv.dll
    - winsrv.dll: its threads runs kernel mode code that handles the raw input thread and dekstop thread
    - sxssrv.dll
    - csrsrv.dll
    - cdd.dll: dll for interactive user sessions only, communicates with kernel's DirectX to draw visible dekstop state without hw-accellerated GDI support
- Win32k.sys, kernel device driver that contains
    - Window manager
    - graphics device interface (GDI)
    - wrappers for DirectX (implemented inside the Dxgkrnl.sys driver)
- conhost.exe that provides support for console applications
- Dwm.exe, desktop window manager , uses CDD and DirectX
- Subsystem DLLs to translate documented WinAPIs into syscalls in Ntoskrnl.exe and Win32k.sys
- graphics device drivers
