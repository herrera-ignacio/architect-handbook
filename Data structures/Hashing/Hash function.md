# Hash function
## Definition
A hash function is any function that can be used to map data of arbitrary size to fixed-size values (though there are some hash functions that support variable-length output).
A hash function may be considered to perform **three functions**:
- Convert variable-length keys into fixed-length values, by folding them by words or other units using a parity-preserving operator like ADD or XOR.
- Scramble the bits of the key so that the resulting values are uniformly distributed over the keyspace.
- Map the key values into ones less than or equal to the size of the table.
### Hash values and digests
The values returned by a hash function are called hash values, hash codes, hash digests, digests, or simply hashes.
The values are usually used to index a fixed-size table called a *hash table*.
## Usage
- **Data storage and retrieval**: Hash functions and their associated hash tables are used in data storage and retrieval applications to access data in a small and nearly constant time per retrieval.
- **Integrity checking**: Identical hash values for different files imply equality, providing a reliable means to detect file modifications.
- **Key derivation**: Minor input changes result in a random-looking output alteration.
- **Message authentication codes** (MACs): Through the integration of a confidential key with the input data, hash functions can generate MACs ensuring the genuineness of the data (e.g., HMACs).
- **Signatures**: Message hashes are signed rather than the whole message.
## What makes a good hash function?
A good hash function satisfies two basic properties:
- Should be very fast to compute.
- Should minimize duplication of output values (collisions).
Hash functions rely on generating favorable probability distributions for their effectiveness, reducing access time to nearly constant.
High table loading factors, pathological key sets, and poorly designed hash functions can result in access times approaching linear in the number of items in the table.
## Collition-resolution
A necessary adjunct to the hash function is a collision-resolution method that employs an auxiliary data structure like linked lists, or systematic probing of the table to find an empty slot.
## Properties
### Uniformity
It should map the expected inputs as evenly as possible over its output range. That is, every hash value should be generated with roughly the same probability.

> [!tip] Uniformly distributed is not random
> This criterion only requires the value to be *uniformly distributed*, not *random* in any sense. A good randomizing function is (barring computational efficiency concerns) generally a good choice as a hash function, but the converse need not be true.
#### Absolute uniformity
In special cases when the keys are known in advance and the key set is static, a hash function can be found that achieves absolute (or collision-less) uniformity. Such a hash function is said to be *perfect*.
There is no algorithmic way of constructing such a function -- searching for one is a factorial function of the number of keys to be mapped versus the number of table slots that they are mapped into.
Finding a perfect hash function over more than a very small set of keys is usually computationally infeasible; the resulting function is likely to be more computationally complex than a standard hash function and provides only a marginal advantage over a function with good statistical properties that yields a minimum number of collisions.
### Testing and measurement
When testing a hash function, the uniformity of the distribution can be evaluated by the [chi-squared test](https://en.wikipedia.org/wiki/Chi-squared_test) which is a goodness-of-fit measure: it's the actual distribution of items in buckets versus the expected distribution of items.
### Efficiency
A hash function takes a finite amount of time to map a potentially large keyspace to a feasible amount of storage space searchable in a bounded amount of time regardless of the number of keys.
In most applications, the hash function should be computable with minimum latency and secondarily in a minimum number of instructions.

> [!tip] Space-time trade-off
> In data storage and retrieval applications, the use of a hash function is a trade-off between search time and data storage space.
> If [memory](https://en.wikipedia.org/wiki/Computer_memory "Computer memory") is infinite, the entire key can be used directly as an index to locate its value with a single memory access. On the other hand, if infinite time is available, values can be stored without regard for their keys, and a [binary search](https://en.wikipedia.org/wiki/Binary_search "Binary search") or [linear search](https://en.wikipedia.org/wiki/Linear_search "Linear search") can be used to retrieve the element.

### Applicability
A hash function that allows only certain table sizes or strings only up to a certain length, or cannot accept a seed, is less useful than one that does.
### Deterministic
A hash procedure **must be deterministic** -- for a given input value, it must always generate the same hash value.
### Defined range
It is often desirable that the output of a hash function have fixed size.