# Processes
Container of resources used when an instance of a program is executed. Includes
- Private virtual address space: range of virtual memory addresses usable by the process
- Executable program that defines initial code and data, mapped inside the process' address space
- List of open hadnles to various system resources
- Security context: an access token that identifies the authorization of the user account associated with the process
- PID: process unique identifier
- Various threads (at lesat one)
- Pointer to the parent or creator process 
	- not always the real creator process
	- if the parent is killed, the information is not updated