# Terminal Services
Support of multiple interactive user sessions on a single system.

First session = services session, session zero. Contains system service hosting processes. Usually it's the first login session at the physical console. Additional sessions are created using remote desktop or fast user switching.

Specific Windows APIs are available to be used by applications that wants to be aware of running in a terminal server session (like `WTSEnumerateProcesses`, used in maldev for as an alternative API for process enumeration)
## Fast user switching
isolates all processes and session wide data structures, while enabling the creation of a new user session. What happens when you "disconnect" instead of "log out"
## Multi user support
- client editions of windows: single user at the same instance, or physical or remote but not both
- server editions of windows: two simultaneous remote connections. more than two if licensed and configured as terminal server.