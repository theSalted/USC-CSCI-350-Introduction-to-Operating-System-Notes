 CSCI 350 - Introduction to Operating System

Professor Tatyana Ryutov (tryutov@usc.edu)

- Course Info
- What is OS
- Address space abstraction
- Process abstraction
- Syscall intro 

TA: Huanyu Chen (huanyuc@usc.edu)

Aditya Hariharan (adityaha@usc.edu)

Required textbooks:
- T1 "Operatinh Systems: Priniciples and Practice", Tomas Anderson, 2nd edition
- T2 "Operating Systems Concepts" by Abraham Silberscatz, 9th edition
- T3 "Distributed Systems" by M. van Steen, 3rd Edition

Piazza
-piazza.com/usc/fall2024/csci350

Deliveriables
- Five programming projects (C language)
    - One is optional
    - For each project will have to answer Free Response Questions
- Required Readings
    - Primarily from the three textbooks
    - You will not be tested on materials in the textbooks that we did not cover in class
    - Recommended(optional) material will be posted

### xv6

xv6is an MIT reimplementation of Linux v6. xv6 is monolithic, preemptively-multitasked, multiprocessor-capable, 32-bit, UNIX-like operating system

Some limitations:
- max addressable memory: 2GB
- few supported devices (e.g. no network)
- no kerneal level threading 
- do it on a vm

Resouces
pdos.csail.mit.edu/6.828

### What is OS

Devices can be useful without system (embeded system, sensors, etc.)

Memory device, Disk Device, Network device, Display device, (hardware)

Process (apps) run on OSes (Spotify, Browsers, Offices, Slack, Databases).

Apps want to interact on hardware, but it's a bad idea to allow apps to run hardware.

OS is the middle man between hadwares and apps. 

OS is a piece of hard ware that stand in the middle between hardwares and apps. OS expose it's capaibility to apps via System Calls (syscalls). On lower level, OSes uses something called Hardware Abstraction Layer (HAL) to interact hardware. Hardware allow hardware to be portable to OSes. A program that run on User Mode (non-previleged) is called apps. A program that run on Kernel Mode (previlged) is called kernel program or drivers (a type of kernel programs).


What is the OS Kernel

**Core Component of OS**
- Has full access to all the HW
Responsible for:
- Process management
- CPU schedueling
- Memory management
- Storage management
- Protection and security
- Device and I/O management (not discussed in class)

*This class focus on kernel*

Core kernel functions:
- Process management
- CPU schedueling
- Memory management
- Storage management
- Protection and security

### OS Challeneges
- Reliability
    - Does the system do what it was designed to do?
- Availability 
    - What portion of the time is the system working?
- Security
    - Can the system be compromised by an attacker?
- Performance
    - Latency (or response time)
        - How long does an operation take to complete
    - Throughput
        - How many operations can be done per unit of time
    - Overhead
        - How much extra work is done by the os
    - Fairness
        - How equal is the perforamnce by different users?
    - Predictability
        - How consistent is the performance over time?
- Portability & adoption

**An ideal os is not achievable**

**OS is a complex mess**
How can we build and understand a complex messy systems?
- Come up with some structure
    1. Manage compelexity throug abstraction (e.g. address space, process, file)
    2. Apply good design principles (e.g. separation of policty from mechanism)
    3. Consider tradeoffs (e.g., optimize for common case)

### Basics of Address Space Abstraction (really high level)
- Early systems did not provide memory abstraction to users
    - Early system have limited memory, and often only run 1 program. Therefore early devices does not provide such abstraction
- Time-sharing demanded OS to implement memory sharing efficiently
    - You can divide memory to different area for each apps
    - Unrestricted memory access mean apps can intentionlly or unitentionally access memory of another apps to corrupt them and to read them.

#### Sidenote: The principle of isolation
- Isolation is a key principle in building reliable system
- If two entities are properly isolated from one another, one can fail without affect the other
(Ships like Titanic, have isolation in their haul as well)

### Assress Space Abstraction
- Abstraction of physical memory
    - Running program's view of physical memory
- Goals:
    - Give each process a private memory area
    - Prevent one process from reading/writing outside its private memory
    - Allow sharing, when needed
- Each process has it's own address space (user space)
- OS has its own address space (kernel space)

Processes are usually isolated in Sandboxes to keep kernel safe

### What is a process?
- Process is not a program (but related to it)
- A process is a program that's running 
- Once a user execute a program, the OS would needd to allocate some memory from the process and CPU would starting to executing the program's instructions
- Process is an istance of a program, running with limited rights
- Processes conssits of two parts:
    - Address space
        - Code, data, stack, heap
    - Current activity represented by Process Control Back (PCB)
        - Program encounter, contents of the processor register, list of open files, etc.
