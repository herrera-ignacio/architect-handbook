# Stacks
## Overview
A stack is an **ordered collection of elements** where elements are only added and removed from the same end (**LIFO - Last In First Out**).
In the physical world, an example of a stack would be a stack of plates in a kitchen - you add plates or remove plates from the top of the pile. In the software world, a good example of a stack is the history of your current browser's tab.
Typically, inserting into a stack is called **pushing** and removing from a stack is called **popping**. Stacks will usually also come with operations like **peek**, which means looking at the element at the top of the stack.
## Implementation
The time complexity of stack operations is dependent on the implementation. If you use a dynamic array, which is the most common and easiest way, then the time complexity of your operations is the same as that of a dynamic array. $O(1)$ push, pop, and random access, and $O(n)$ search. Sometimes, a stack may be implemented with a linked list with a tail pointer.
## When to use it?
For algorithm problems, a stack is a good option whenever you can recognize the LIFO pattern. Usually, there will be some component of the problem that involves elements in the input interacting with each other.
Interacting could mean matching elements together, querying some property such as "how far is the next largest element", evaluating a mathematical equation given as a string, just comparing elements against each other, or any other abstract interaction.