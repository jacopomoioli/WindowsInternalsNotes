# Virtualization Based Security Overview

User / Kernel modes separation is well defined, but a compromised driver is enough to compromise the whole system at kernel level.

Virtualization based security creates a new security bounduary by introducing VTLs (Virtual Trust Levels):
- VTL 0: 
    - User mode (Ring 3)
    - Regular kernel & drivers (Ring 0)
- VTL 1: 
    - Isolated User Mode (IUM) (Ring 3)
    - Secure Kernel (Ring 0)

Both VLTs are built on top of Hyper-V.

4 different "areas", isolated by each others. Some examples:
- VTL0 kernel cannot interact with user mode VTL1 because VTL1 is more privileged
- VTL1 user mode cannot interact with VTL0 kernel because IUM is on ring3 while VTL0 kernel on ring0
=> Rings enforce POWER, VTLs enforce ISOLATION

- VLT1 Ring0: can access everything on both rings and VTLs (thanks an thru the hypervisor)
    - only entity that can configure SLAT (Second Level Address Translation): tell the hypervisor to limit the access of VLT0 Ring3 to specified memory regions
- VLT0 Ring0: can access everything in VLT0 only (VLT1 is completely isolated)
- VLT1 Ring3: can access directly only itself, but it can interact with VLT1 Ring0
- VLT0 Ring3: least powerful

I/O MMU (Memory Management Unit) prevents VLT0 Ring0 device drivers to access physical memory directly (and bypass VLTs and SLAT because no logical addresses) by virtualizing the memory access from the devices.

Inside the VLT1 Ring3 (IUM) only special, MS-signed binaries (called **Trustlets**) are allowed to run. Secure kernel (editable only by MS) has a sort of "trustlet allow list", so it's impossible to add a new trustlet (if you aren't microsoft) or tamper an existing one (it would make the signature invalid).


## IUM 
- Environment with restrictions about allowed syscalls usable by regular usermode DLLs
- Framework that offers special syscalls executable only under VLT1 exposed via `Iumbase.dll` (VLT1 version of `KernelBase.dll`)

## Secure Kernel
Its own separate binary (`securekernel.exe` on disk)


