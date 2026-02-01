# Key System Components

## Environment Subsystems
Each env subsystems provides a different subset of native windows services. Each executable image is bound to a single subsystem, specified with the linker's `SUBSYSTEM` option.

Usermode applications do not call native syscalls directly, but they go thru one or more subsystems DLLs, e.g. kernel32.dll, advapi32.dll, user32.dll, gdi32.dll. When a subsystem dll's function is invoked, three different options:
1) Function is entirely implemented in user-mode
2) Function requires the use of one or more native syscalls
    - e.g. `ReadFile` calls the undocumented, native, internal `NtReadFile`, `WriteFile` calls `NtWriteFile` 
3) Function requires the execution of a task in the environment subsystem process. A client/server request is sent to the environment subsystem via a ALPC message.

Sometimes, both 2 and 3.
