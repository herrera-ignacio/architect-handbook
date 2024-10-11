# Mutlithreading

Mutlithreading is a programming and execution model that allows __multiple threads to exist within the context of one process__. These threads share the process's resources, but are able to execute independently. Multithreading can also be applied to one process to enable __parellel execution__ on a multiprocessing system.

The threaded programming model provides developers with a useful abstraction of concurrent execution.

## Advantages

* __Responsiveness__: allow an application to remain responsive to input by moving long-running tasks to a _worker thread_ that runs concurrently with the main execution thread.
* __Faster execution__: program can operate faster on computer systems that have multiple CPUs or one or more multi-core processors, or across a cluster of machines, because threads of program naturally lend themselves to parallel execution, assuming sufficient independence.
* __Lower resource consumption__: application can serve multiple clients concurrently using fewer resources than it would need when using multiple process copies of itself. For example Apache HTTP Server uses thread pools.
* __Better system utilization__: as an example, file system using multiple threads can achieve higher throughput and lower latency since data in a faster medium (such as cache memory) can be retrieved by one thread while another thread retrieves data from a slower medium with neiter thread waiting for the other to finish.
* __Simplified sharing and communication__: unlike process, which require a message passing or shared memory mechanism to perform inter-process comunication, threads can communicate through data, code and files they already share.
* __Parallelization__: applications can split data and tasks into parallel subtasks and let the underlying architecture manage how the threads run, either concurrently on one core or in parallel on multiple cores.

## Drawbacks

* __Synchronization__: threads share the same address space, so programmer must be careful to avoid __race conditions__ and other non-intuitive behaviors. Threads will often need to rendezvous in time, in order to process the data in the correct order. Threads may also require mutually exclusive operations to prevent common data from being read or overwritten in one thread while being modified by another. Careless use of such primitives can lead to __deadlocks, livelocks or races over resources__.
* __Thread crashes a process__: an illegal operation performed b a thread crashes the entire process, therefore, one misbehaving thread can disrupt the processing of all others.

## Vs Multiprocessing

Multiprocessing differs in:

* Requires no synchrnization (processes run in different address spaces)
* OS prevents processes from writing to another processes' address space.
* Address spaces large, thus processes can take up much more memory.

## Implementation

### Single processor systems

Systems with a single processor generally implement multithreading by __time slicing__.

The CPU (Central Processing Unit) switches between different software threads. This __context switching__ generally happens very often and rapidly enough that users perceive the threads or tasks running in parallel.

On a processor or core with __hardware threads__ separate software threads can also be executed __concurrently__ by separate hardware threads.

### Multiprocessor or multi-core systems

Multiple threads can execute in __parallel__, with every processor or core executing a separate thread simultaneously, and those processor/core can also have hardware threads.

### OS Implementations

Process schedulers of many modern operating systems directly support both time-sliced and multiprocessor threading, and the operating system kernel allows programmers to manipulate threads by exposing required functionality through the __system-call interface__.

Some threading implementations are called __kernel threads__, whereas __light-weight processes (LWP)__ are a specific type of kernel thread that share the same state and information. Furthermore, programs can have __user-space threads__ when threading with timers, signals, or orther methods to interrupt their own execution, performing a sort of __ad-hoc slicing__.
