# The Rehashing Problem

If you have $n$ cache servers, a common way to balance the load is to use the following hash method: `serverIndex = hash(key) % N`, where `N` is the size of the server pool.

For example, if we have 4 servers and 8 string keys with their hashes, to fetch the server where a key is stored, we perform the modular operation: `f(key) % 4`. For instance, `hash(key0) % 4 = 1` means a client must contact server 1 to fetch the cached data.

| key  | hash     | hash % 4 |
|------|----------|----------|
| key0 | 18358617 | 1        |
| key1 | 26143584 | 0        |
| key2 | 18131146 | 2        |
| key3 | 35863496 | 0        |
| key4 | 34085809 | 1        |
| key5 | 27581703 | 3        |
| key6 | 38164978 | 2        |
| key7 | 22530351 | 3        |

* Server 0: key1, key3
* Server 1: key0, key4
* Server 2: key2, key6
* Server 3: key5, key7

This approach works well when the size of the server pool is fixed, and the **data distribution is even**. However, **problems arise when new servers are added, or existing servers are removed**. For example, if server 1 goes offline, the size of the server pool becomes 3. Using the same hash function, we get the same hash value for a key. But applying moduler operation gives us different server indexes.

| key  | hash     | hash % 3 |
|------|----------|----------|
| key0 | 18358617 | 0        |
| key1 | 26143584 | 0        |
| key2 | 18131146 | 1        |
| key3 | 35863496 | 2        |
| key4 | 34085809 | 1        |
| key5 | 27581703 | 0        |
| key6 | 38164978 | 1        |
| key7 | 22530351 | 0        |

* Server 0: *key0*, key1, *key5*, *key7*
* _Server 1: Removed_
* Server 2: key2, *key4*, key6
* Server 3: *key3*

Most keys are **redistributed**, not just the ones originally stored in the offline server 1. This means that when server 1 goes offline, most cache clients will connect to the wrong servers to fetch data. This causes a **storm of cache misses**. *Consistent hashing* is an effective technique to mitigate this problem.
