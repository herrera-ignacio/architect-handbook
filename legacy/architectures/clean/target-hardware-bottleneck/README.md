# Target-Hardware Bottleneck

When embedded code is structured without applying clean architecture principles and practices, you will often face the scenario in which you can test your code only on the target. If the target is the only place where testing is possible, the target-hardware bottleneck will slow you down.

> A *clean embedded architecture is a testable embedded architecture*, and its testable *off* the target hardware.

The line between software and firmware is typically not so well defined as the line between code and hardware. One of your jobs as an embedded software developer is to firm up that line.

The name between the software and the firmware is the *Hardware Abstraction Layer (HAL)*.

The HAL exists for the software that sits on top of it, and its API should be tailored to that software's need.

> A successful HAL provides that seam or set of substitution points that facilitate off-target testing. 
