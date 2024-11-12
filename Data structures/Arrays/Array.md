# What is an array?
## Definition
An array is a collection of items stored at contiguous memory locations. The idea is to store multiple items of the same type together. This makes it easier to calculate the position of each element by simply adding an offset to a base value (i.e., the memory location of the first element of the array).
![[Pasted image 20241111172708.png]]
## Operations
In terms of algorithm problems, arrays (1D) and strings are very similar: they both represent an ordered group of elements.

| Operation                  | Array/List | String (immutable) |
| -------------------------- | ---------- | ------------------ |
| Appending to end           | \*O(1)     | O(n)               |
| Popping from end           | O(1)       | O(n)               |
| Insertion, not from end    | O(n)       | O(n)               |
| Deletion, not from end     | O(n)       | O(n)               |
| Modifying an element       | O(1)       | O(n)               |
| Random access              | O(1)       | O(1)               |
| Checking if element exists | O(n)       | O(n)               |
> [!tip]
> Appending to the end of a list is [amortized O(1)](https://stackoverflow.com/questions/33044883/why-is-the-time-complexity-of-pythons-list-append-method-o1).
## Applications
1. Store data elements of the same data type.
2. CPU Scheduling.
3. Implement other data structures like Stacks, Queues, Heaps, Hash tables, etc.
## Language-specifics
"Array" can mean something different between languages. For example, Python primarily uses "lists" instead of arrays which are extremely lenient. Initialization is as easy as `arr = []`, and you don't need to worry about the type of data you store in the list or the size of the list. Other languages like C++ require you to specify the size and data type of the array during initialization, but also have support for lists (like `std::vector` in C++).

t's important to know the details behind arrays for the language you plan on using in interviews.