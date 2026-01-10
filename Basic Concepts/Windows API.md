
# Windows API
User-mode system programming interface. Historically:
- Win16: 16-bit windows APIs
- Win32: API for 32-bit windows versions (>NT)
- Win64: modern APIs
*WinAPI* generically refers to both Win32 & Win64.

Lots of "flavors": Originally, only C-Style functions. With time, naming inconsistency and different logical grouping. Today:

## #COM: Component Object Model
Originally created for MS Office applications to exchange data between documents using #OLE: Object Linking and Embedding (what made possible to embed a excel graph into a word document, etc.)

COM principles:
- **Clients** communicate with **Objects** (AKA COM server objects) thru **Interfaces**
- Interfaces are defined contracts with related methods grouped under the virtual table dispatch mechanism => Binary compatibility
- **COM Server**: DLLs or EXEs where COM classes are implemented

## #WinRT: Windows Runtime
Introduced with Windows 8, services for "Windows Apps" (FKA Metro apps, modern apps, immersive apps, windows store apps, and god knows what else).
Built on top of COM, with some extensions.
- Normal windows programs (non-windows apps, now called "Windows Desktop Applications") can use a subset of WinRT APIs
- Windows apps can use a subset of standard Win32 and COM APIs
Generally based on top of legacy APIs, it's not a new and isolated native API.

## .NET Framework ( #dotNET)
Part of Windows, basically composed by
- CLR
- FCL

![[Pasted image 20260110190839.png]]
### CLR: Common Language Runtime
runtime engine for .NET, includes 
- a JIT compiler that translates CIL (Common intermediate language, a sort of bytecode) instructions to machine language
- garbage collector
- type verification
Implemented as a COM in-process server (DLL), uses WinAPI

### FCL: .NET Framework Class Library
Collection of types that implement functionalities needed by applications, such as GUI, networking, db access, etc.
