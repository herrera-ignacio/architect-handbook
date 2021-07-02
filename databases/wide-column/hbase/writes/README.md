# HBase Write Mechanism

![](2021-07-02-13-56-39.png)

1. When a client issues a *put* request, it will write the data to the *WAL*.

> *Write Ahead Log (WAL)* is a file used to store new data that is yet to be put on permanent storage. It is used for recovery in the case of failure.

2. Once data is written to the WAL, it is then copied to the *MemStore*

> *MemStore* is the write cache that stores new data that has not yet been written to disk. There is one MemStore per column family per region.

3. Once the data is placed in *MemStore*, the client then receives the ACK (*acknowledgement*)

4. When the *MemStore* reaches the threshold, it dumps or commits the data into a HFile.

> *Hfiles* store store the rows of data as stored KeyValue on disk.
