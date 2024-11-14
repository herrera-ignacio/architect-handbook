# Sets
## Definition
A set is an **unordered** abstract data type that can **store unique values**. It is a computer implementation of the mathematical concept of a *finite set*.

> [!tip] Test membership
> Unlike most other collection types, rather than retrieving a specific element from a set, one typically tests a value for membership in a set.
## Advantages
You can add, remove, and check if an element exists in a set in $O(1)$.
## Sets vs hash table
Sets use the same mechanism for hashing keys into integers but the difference is that sets do not map their keys to anything.
Sets are convenient to use when you only care about checking if element exists.