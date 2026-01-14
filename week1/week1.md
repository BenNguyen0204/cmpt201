# Week 1 - A Tour of Computer Systems

## System programming:
- Low-level programming that interacts with OS/hardware via syscalls
- Low-level languages are C, C++, Rust
- **Syscall interface** = API boundary between apps and kernel

## OS Stack: 
    - Applications (user programs)
    - Kernel (core OS services)
    - Hardware (CPU, memory, I/O)

### Hardware Basics (Von Neumann):
- Two fundamental components: computation (CPU) + data (memory/storage)
- CPU fetches data/instructions from memory
- Main hardware parts: CPU, memory, I/O devices

#### CPU + Memory Trends (Moore’s Law shift):
    - Pre-2000s: frequency growth
    - Post-2005: more cores (multi-core)
    - CPU faster than RAM → CPU–memory gap
    - Memory limited by chip speed + physical distance

#### Memory hierarchy (why caches exist)
- Caches reduce CPU–memory gap by keeping frequently used data closer to CPU
- L1 (fastest/smallest) → L2 → L3 (biggest/slowest cache)
- Fast = small/expensive/close, Slow = large/cheap/far
- Ex: Registers → L1/L2/L3 Cache → RAM → SSD → HDD → 
- **Trade off**
    - Cost: Bigger size -> more expensive
    - Distance and access speed: faster -> closer to CPU
    - Persistence: "commit" means moving data from memory to disk
    - Reliability: SSD vs HDD vs tape: SSD's fastest but least reliable

#### CPU Architectures
- ISA = instruction set (x86, ARM, RISC-V)
- Compiler turns C code into ISA machine instructions

#### 32-bit vs 64-bit register size
- Register size = pointer variable size
- Register/pointer size = 32 vs 64 bits
- Pointer size limits max addressable memory
- Wider bus needs more wires for address + data transfer

#### Memory + addressing
- Memory is byte-addressed (each address points to 1 byte)
- If memory has N bytes, you need log2(N) address bits
- 32-bit address space: 2^32 bytes = 4GB
- 64-bit address space: extremely large (most computers are 64-bit architectures now)

### Kernel (what the OS does)
- OS = kernel + tools (shell/GUI/utilities)
- Handles CPU scheduling, memory management, devices & I/O, file system, networking, and security.
- Protection/isolation between programs

#### Kernel is event-driven
- Kernel reacts to events like:
    - Interrupts (keyboard, disk, network)
    - Syscalls (program requests service)
    - Exception signals (errors like division by zero)

#### User mode vs kernel mode
- *User mode*: limited privileges (apps run here)
    - *Root user*: admin powers, still not kernel-only memory/instructions.
- *Kernel mode (Ring 0)*: full privileges (kernel runs here)
- Purpose: safety + isolation (apps can’t directly control hardware).

Major OS abstractions

Process = running program with its own resources

Threads = execution paths inside a process

Virtual memory = each process sees its own “private” address space

File abstraction: many things are treated like files (read/write)

Program → process pipeline

Source code → compiler → executable machine code → loaded into memory → running process

Compiled (C/C++): fast, but machine-specific binary

Interpreted (Python): portable, slower

Hybrid/VM style: compile to intermediate form (bytecode) then run/translate

POSIX + portability

POSIX = standard interface for Unix-like OSes

Helps code run across Linux/macOS with minimal changes

Virtualization vs containers

Virtual machines: emulate full machine/OS environment

Containers: isolate apps but share the host kernel (lighter than VMs)