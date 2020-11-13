# Processes & Threads

A quick way to understand this is that:

* __Thread__: State of a program.
* __Process__: Program + the state of all threads executing in the program.

## Definitions

### Process

Process means __any program in execution__. There's a process _Control block_ which controls the operation of any process and contains information about them, such as priority, id, state, cpu, register, etc. One characteristic of process is that it is __isolated__, meaning that a process __does not share memory with any other process__. Thus, each process has its own _Control Block_, Stack and Address Space.

Processes switching uses interface in operating system (they iteract only through system-provided inter-process communication mechanisms), so context switching is more expensive than with threads. If one server process is blocked no other server process can execute until the first one is unlocked.

A process can create other processes which are known as __Child Processess__.

### Thread

It can be defined as the smallest sequence of programmed instructions that can be managed independently by a scheduler. Implementation of threads and processes differs between operating systems, but in most cases, a thread is a __segment of a process__. Thus, a process can have multiple threads that can be executed __concurrently__ and __share resources__ such as memory.

In particular, threads of a process share its executable code and the values of its dynamically allocated variables, and non-thread-local global variables at any given time.

Unlike processes: 

* Threads are not isolated and can share memory.
* Consume less resources, and takes less time both to create and to terminate.
* Is more efficient in term of comunication, taking less time for context switching.
* If one server thread is blocked, a second thread in the same process could run.
* Thread has parent process' _Control Block_, but also, its own thread control block, Stack, and common Address Space.

A thread has 3 states:

* Running
* Ready
* Blocked


