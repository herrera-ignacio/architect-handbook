# Hash map
## Definition
A hash map (also known as hash table or dictionary) is an **unordered data structure that stores key-value pairs**.
It implements an associative array, which is an abstract data type that maps keys to values. It uses a [[Hash function]] to compute an *index*, into an array of *buckets* or *slots*, from which the desired value can be found.
![[Pasted image 20241114124706.png]]
Typically, the only constraint on a hash map's key is that it has to be **immutable**.
## Advantages
- It allows to reduce the time complexity of a search algorithm by a factor of $O(n)$ for a huge amount of problems.
- It can add, update, check if exists and remove elements in $O(1)$.
## Disadvantages
- For smaller input sizes, they can be slower due to overhead.
- Can take up more space than arrays.
- When implemented using a fixed size array, resizing is much more expensive than a normal array because every existing key needs to be re-hashed, and a hash table may use an array that is significantly larger than the number of elements stored, resulting in a huge waste of space.