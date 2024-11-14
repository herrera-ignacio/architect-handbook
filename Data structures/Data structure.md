# Data structures

## What is a data structure?
A data structure is a data organization and storage format for efficient access to data. More precisely, it's a collection of data values, the relationships among them, and the operations that can be applied to the data (i.e., it's an *algebraic structure* about data).
We can split data structures into two things: the interface and the implementation.
## Interface
The interface is like a contract that specifies how we can interact with the data structure -- what operations we can perform on it, what inputs it expects, and what outputs we can expect.
For example, consider a dynamic array. The interface would include operations like appending, insertion, removal, updating, and more.
## Implementation
The implementation is the code that actually makes the data structure work. It includes the details of how the data is stored and how the operations are performed.
For example, the implementation of a dynamic array might involve allocating memory for the list, tracking the size, and rearranging the elements when an operation like remove is called.