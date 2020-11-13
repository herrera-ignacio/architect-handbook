# Parallelism vs Concurrency

![visual](https://techdifferences.com/wp-content/uploads/2017/12/Untitled.jpg)

## Parallelism.

Parallelism is about _doing multiple things at the same time_.

For this, it uses multiple CPUs/cores to operate multiple processes/threads. Thus, results in overlaping of CPU and I/O activities in one process/thread with the CPU and I/O activities of another process/thread.

## Concurrency

Concurrency is about _dealing with multiple things at the same time_ (giving the illusion of simultaneity).

Scheduler __interleaves threads__ (context switching), and how much time each thread gets is non-deterministic and not in developers control, so which instructions are being run by a thread is also non-deterministic. Thus, in concurrency scenarios, it's important to look for threads to coordinate, generally using locks.

* Shared resource is to be access/updates.
* Multiple tasks need to coordinate.

## Concurrency + Parallelism

* Split the sequential flow into independent components.
* Use threads/threadpools to parallelize (speed up).
* Whenever share resource is to be updated, use concurrency tools to manage state.
* Whenever independent components need to coordinate, use concurrency tools.
