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

VTL1 user mode applications are not more powerful, just isolated from VLT0 user mode; 
VLT1 kernel mode is the most powerful (VLT1 & ring0), and has complete access on VLT0

## IUM 
- Environment with restrictions about allowed syscalls usable by regular usermode DLLs
- Framework that offers special syscalls executable only under VLT1 exposed via `Iumbase.dll` (VLT1 version of `KernelBase.dll`)

## Secure Kernel
Its own separate binary (`securekernel.exe` on disk)


