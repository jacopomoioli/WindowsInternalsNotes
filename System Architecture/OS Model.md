Windows is a monolithic OS: OS core and device drivers share the kernel-mode memory space: any OS component or device driver can potentially crash the whole core. Windows addresses these problems thru
- WHQL: Windows Hardware Quality Labs: microsoft testing and subsequent certification of third party drivers 
- Microsoft Hardware Developmer Program
- KMCS: Kernel Mode Code Signing
- Device Guard
- Hyper Guard