# System Calls

            <-         interrupt    <-
embrio -> admitted -> runnable -> running -> zombie
            <-         waiting     <-


## Protection

Need for protection
- Kernel can't trust user processes which may be mailicous or buggy
- Kernel must proyecy
    - User processess from one anoter
    - Kernal from user processes
- Isolating processes from another is key to protectiojn

HW mechnisms for protecion:
1. Memory protectin (will cover later)
-  Segmentation and paging


## Dual Mode Operation
Goal: distinguish between execution of trusted OS code and untrusted user code
Two Processor Modes:
1. Kernal Mode
    - Execution with full privileges of HW
    - No memory access limtis
2. User mode
    - Limit privileges
    - Limits on memory accesses

Instructions available in kernel mode, but not in user mode, are previleged instructions
Privileges instructions
- Examples:
    - Changes with memory locations a user program can access
    - Send commands to I/O devices
    - Read data from/writre data to I/O

ARM has seven basics modes (but most hardware instructions et ave least two modes

## HW Protections Rings
Generalization of user/kernel modes

Define a fixed number N of hierarchial domains (called protection rings
- Named by intergrs 0 through N-1
- Access capabilities available in ring m are a subset of those in ring n, m > n


## User and kernel stacks
In most OSs each process has two stacks
- User stack (used when executing user code)
- Kernel stack (used when executing kernel code) (to prevent user crash to kernel crash)

## Context Switch 
Switching CPU from one running task to another by saving the CPU state to resume the task


## x86 Registers

Small space for data storage within CPU
- **general purpose registers**: store data during computations (edx...)

- **Caller** is a function that calls another function
- **Callee** is a function that was called


