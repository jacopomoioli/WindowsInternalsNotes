# Kernel Debugging
Examining kernel data structures and stepping thru kernel functions execution.

## Requirements
### Kernel Symbols
Contains 
- names of functions
- names of variables
- data structures layout and format

Needed the symbols of `ntoskrnl.exe` matching the debugged version. 
Microsoft maintains a symbol server to make this easier: https://msdl.microsoft.com/download/symbols

### Debugging Tools for Windows
Contains four debuggers
- cdb, ntsd: console-based, user-mode debuggers
- kd: console-based, kernel-mode debugger
- WinDbg: GUI-based debugger for both kernel and user-mode
All equivalent, because based on the same underlying engine (`DbgEng.dll`)

### Windows Software Development Kit
Contains windows API headers files, SDK tools and documentation.

### Windows Driver Kit
really useful documentation and header files

# User Mode Debugging
2 modes
### Invasive
attach on a running process using `DebugActiveProcess`.
Most powerful mode, possible to examine and change process memory, set breakpoints, etc.
### Noninvasive
Debugger opens the target process with `OpenProcess`.
Possible to examine and edit memory in the target, but cannot set breakpoints.

## Kernel Mode Debugging
3 types of kernel debugging (+1)
- Passive: open a crash dump file created after a system crash
- Remote Live: connect to a running system, examine system state, set breakpoints on device driver code. 
	- 2 computers needed: target (debugged computer, booted in debugging mode via `bcdedit.exe`) and host (debuggee)
- Local Live: examine local system state. Some limitations (e.g. cannot set breakpoints, needs debug mode)
- LiveKD: utility that creates and updates in real time a dump file. The debugger open this file thinking it's a static dump, but in reality the content is coming from the live system and real-time-updated. No reboot, no debugging mode required