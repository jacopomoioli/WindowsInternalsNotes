# Virtualization Based Security
> Lots of things changed.

Win10 uses the Hyper-V hypervisor to provide a set of features known as VBS:
- HVCI - Memory Integrity: runs kernel mode code integrity checks inside the VBS secure container
- Credential guard: isolates secrets and credentials in a protected virtual environment, LSA ISO
- System Guard: Secure Launch

Previously, it provided:
- Credential Guard: Prevents unauthorized access to credentials and secrets
- Core isolation: ex Hyper Guard, protects key data structures and code related to the kernel and the hypervisor
- Device Guard
- Application guard: Historically used as a sandbox for Microsoft Edge & office, deprecated and removed since Win11 24H2