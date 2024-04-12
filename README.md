## User vs Kernel 
* The kernel is the part of the operating system that runs with higher priviliges, code that runs in kernel mode can fully control the CPU.  
* The user means by applications running with low priviligies, code in user mode has certain limitations. 
* The kernel space is the memory area that is reserved to the kernel, it is accessed protected so that user applications can not access it directly.  
* Thre user space is the memory area reserved to a particular user process, it can be directly accessed from code running in kernel mode.
## Typical operating system architecture 
* The kernel is responsible for **access** and **sharing** the hardware in a secure and fair manner with multiple applications.  
* System calls are the interface between a user-space applicatin and the operating system kernel, allowing user-level processes to request services from the kernel, such as performing I\O operations, managing files, allocating memory, creating processes..
* Regardless of the hardware architecture or specific implementation details, they provide a standarized way for application to interact with the underlying operating systems.   
![image](https://github.com/GhassenHafsiaINSAT/linux-kernel-labs/assets/110825502/cb180af0-1ea7-4fdf-b2e6-1491294c946e)
### Monolithic Kernel 
* In a monolithic kernel architecture, the entire operating system kernel is implemented as a single piece of software.
* All core operating system functions, such as process management, memory management, file system management, device drivers, and system calls, reside within the kernel's address space.
* Communication between different kernel components is done through direct function calls and data structures.  
![image](https://github.com/GhassenHafsiaINSAT/linux-kernel-labs/assets/110825502/e155f317-939b-4daa-8532-99f4178c6643).
### Micro Kernel 
* In a microkernel architecture, the kernel is kept as small as possible, with only the essential functions, such as process scheduling, inter-process communication (IPC), and basic memory management, implemented in the kernel.
* Additional functionality, such as device drivers, file systems, and networking protocols, are implemented as separate user-space processes or modules, running outside the kernel's address space.
![image](https://github.com/GhassenHafsiaINSAT/linux-kernel-labs/assets/110825502/32bc2e57-3af8-4393-a6a2-154b312aef7f)

### Monolithic Kernel vs Micro Kernel 
* Monolithic kernels incorporate most operating system functions directly into the kernel, while microkernels keep the kernel minimal and delegate additional functionality to user-space processes or modules.

## Address space 
* The physical address space refers to the actual hardware memory addresses.  
*  The virtual address space provides an abstract view of memory for processes and the kernel. * The process address space is private to each process, while the kernel address space is shared among all processes and managed by the operating system kernel.

## User and Kernel sharing virtual adress space
* The Kernel creates mappings (establishing a relationship between virtual adresses used by a process and the correspending physical memory adresses) that prevent user processes from accessing the kernel space in order to protect critical kernel data structures and preventing unauthorized modifications.
  
## Execution contexts 
* Execution context refers to the different **modes** in which code can execute, each with its own set of privileges, constraints and resposabilities.
### Interrupt context: 
* **Interrupts** are signals sent by **hardware devices** (keyboard presses, network adapters..) or **software** (system calls, exceptions..) to the processor to notify the system of an event that requires immediate handling. 
* When interrupt occurs, the processor temporarily suspends its current execution and transfers control to a speicifc interrupt handler routine (**ISR**) to handle the interrupt.
* Code running in interrupt context always runs in kernel mode with unrestricted access to system ressources and can execut priviliged instructions.
### Process context: 
* It is the environment in which code executes as part of process (user mode / kernel mode)
* in user mode, the process has limited access to system ressources (hardware devices) and can not perform certain priviliged operations, while in kernel mode, the process gains elevated privileges and has direct access to system resources.
*  User-level programs : Text editors, Web brousers and Games.
*  kernel-level programs : accessing hardware, interacting with the operating system.

## Multi-tasking 
* Multitasking is the ability of the operating system to execute multiple programs simultaneously, it is possible by switching rapidly between processes.
* **cooperative multitasking** : the kernel relies on ccoperative schuduling,the programs share control of the CPU.
* **preemptive multitasking** : The operating system sets time limits for each program, if a program runs for too long, the operating system gives other programs a chance to run, it prevents the program from **hogging** all the CPU time.

## Preemptive Kernel 
* A process is preemptive if it can be interrupted by the operating system while running. 
* A Kernel is preemptive if a process can be preemptive while running in kernel mode.
* A kernel may support preemptive multitasking (using timers).

## Pageable Kernel Memory : 
supporting pageable kernel memory means when that parts of kernel's memory, including its code, stack or dynamic allocated memory can be temporarily swapped out to disk when they are not actively used, this process called **Swapping mechanism** and prevents memory exhaustion. 

## Kernel Stack 
* Kernel stack provides a dedicated space for executing kernel code, handling interrupts, managing process state and storing temporary data structures.
* Each process has a kernel stack.  
* Kernel stack ensures the execution of kernel functions while maintaining isolation between processes.

## Portability 
**Modern kernels are composed of :**
* **Architecture and machine specific code** : This section contains code that is specific to a particular computer architecture, includes low-level routines, hardware initialization code. It is written in both C and assembly language.
* **Independent Architecture Code** : This section contains commun components across different architectures (kernel/device drivers), it is written in C language.

## Multiprocessing 
* Multiprocessing refers to the ability of a computer to execute multiple processes simultaneously, using CPU cores.  
### Asymmetric MultiProcessing 
* The primary CPU (master) responsible for running the operating system and managing system ressources, while other CPUs are dedicated to specific tasks or functions.
* Used for embedded systems, real-time applications, where tasks have different requirement and priorities.
![image](https://github.com/GhassenHafsiaINSAT/linux-kernel-labs/assets/110825502/33b1af6a-073b-441f-b6c1-1ad37cc29371)

### Symetric MultiProcessing 
* All CPUs are treated equally and have equal acess to system ressources.  
* tasks are parallelized and executed concurrently across multiple CPU cores.
![image](https://github.com/GhassenHafsiaINSAT/linux-kernel-labs/assets/110825502/8b5f798d-8748-4029-bb13-ae59f22ddc92)

## CPU scalability 
* It refers to the ability of a computer to utilize additional CPU cores as the system workload increases. 


  

