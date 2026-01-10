# Threads
Schedulable entity within a process that is responsible for code execution. A thread includes
- State of the processors (contents of a set of CPU registers)
- 2 stacks
	- Kernel mode stack
	- User mode stack
- Thread-Local storage: a private storage area
- TID: thread unique id
- security context: sometimes it's different that the one of the parent process.

Structure of the thread is architecture-specific and known as "context". WinAPI `GetThreadContext` provides access to it in the CONTEXT block.

The switching between two threads involves kernel scheduler, and it's computationally expensive. because of that, Windows implements two mechanisms: fibers and user-mode scheduling

## Fibers (aka Lightweight threads)
User mode mechanism (therefore invisible to the kernel) that allow an application to schedule its own threads of execution instead of relying on the built-in scheduler.
Implemented in Kernel32.dll.

How it works:
1) call `ConvertThreadToFiber` to convert the current thread to a running fiber
2) create additional fiber using `CreateFiber` WinAPI
3) execute a fiber using `SwitchToFiber` function

Several problems
- invisible to the kernel
- sharing issues of the thread local storage
- cannot run concurrently
